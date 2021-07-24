---
layout: post
title: MSSQL and Java timestamp issue 
date: 2020-06-03 08:00:00:00 +0600
description: MSSQL 2016 and above have issue with java and datetime
img: 2020-06-04-mssql.jpg # Add image post (optional)
fig-caption: MSQSQL 2016# Add figcaption (optional)
tags: [java, hibernate, mssql2016, datetime, datetime2]
---

# The issue
## I cannot query by timestamp in MSSQL 2016
The issue itself is that making queries to a MSSQL 2016 database will break if you are using a timestamp, the problem is that starting in MSSQL 2016 datetime has been upgraded to provided more accuracy for the datetime fields

This can be easily seen in the following query:

{% highlight sql %}
select cast (SYSDATETIME ( ) as datetime) as my_datetime,  cast (SYSDATETIME ( ) as datetime2) as my_datetime2
{% endhighlight %}

| my_datetime             | my_datetime2                |
|-------------------------|-----------------------------|
| 2020-06-05 14:05:07.123 | 2020-06-05 14:05:07.1224577 |


You can notice how *datetime* includes only 3 digits in the millisecond field while *datetime2* includes 7, so is 123 equal to 1224577? Not according to MSSQL
My personal thinking is that MSSQL should be smart enough to cast according to the driver version but according to the documentation the problem comes because java has only 1 SQL field type for timestamp (java.sql.Timestamp), 
so they decided to upgrade the field type without a warning (I mean you could have kept this between JDBC versions) 

The MSSQL 2016 datetime documentation mentions the differences between accuracy


# My Issue 
## How it started
I was making some changes to an old java application, this application uses Spring JPA repostories which has some convenient features but the one in interest here is "save", 
which figure out for you if you are trying to INSERT or UPDATE your entity by using only 1 method (Although this is not the only way to implement this behavior, this is the way it was implemented for this application)

{% highlight java %}
@Transactional(readOnly = true) 
public interface CustomerRepository extends JpaRepository<Customer, Long> {

  Page<Customer> findByLastname(String lastname, Pageable pageable); 
}
{% endhighlight %}

I made a couple changes and this code was working perfectly fine in one of my environments but it was failing in a second environment (Classic developer complaining becuase it works fine in his computer - Everyone) 


# How I found it
I started looking in hibernate and how it was trying to do the save, maybe you are already aware of this but when you invoke the *save* method, hibernate will
1) Try to fine the PK in the cache
2) Try to find the PK in the DB
3) If found, then update
4) If NOT found, then insert

It was always inserting, I had a table with a composed key which included some string, number and the timestamp, but then I noticed that during the query phase it was not finding the entity, why?

[2020-06-02 11:06:17,323] WebContainer : 0 org.hibernate.loader.Loader DEBUG - Bound [8] parameters total
[2020-06-02 11:06:17,382] WebContainer : 0 org.hibernate.jdbc.AbstractBatcher DEBUG - about to open ResultSet (open ResultSets: 0, globally: 0)
[2020-06-02 11:06:17,382] WebContainer : 0 org.hibernate.loader.Loader DEBUG - processing result set
[2020-06-02 11:06:17,383] WebContainer : 0 org.hibernate.loader.Loader DEBUG - done processing result set **(0 rows)**

### Let's create the same query
So I decided to run the same query

I tried everything from strings, date, calendar, different timezones
- Date: 0 rows
- Calendar: 0 rows
- Calendar with different timezone, because someone mentioned UTC was the standard: 0 rows
- String: 1 row, *for some reason I can't understand if you pass a string, it will be casted correctly*

I believe that the real test is to *select* you row by some other field and then try again with your *timestamp* and so I did

{% highlight java %}
package mssql;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Timestamp;
import java.util.Calendar;
import java.util.TimeZone;

public class MySelectTest {

    // Connect to your database.
    // Replace server name, username, and password with your credentials
    public static void main(String[] args) {
       
    	
    	String connectionUrl = "jdbc:sqlserver://<hostname>:<PORT>;databaseName=<DBNAME>;" +
    			"user=<myuser>;" +
    			"password=<mypassword>;" +
    			"encrypt=true;" +
    			"trustServerCertificate=true;";

    	StringBuilder sbSelect1 = new StringBuilder();
    	sbSelect1.append("select "); 
    	sbSelect1.append("* "); 
    	sbSelect1.append("from MY_TABLE mytable"); 
    	sbSelect1.append("and mytable.otherKey = ? ");
    	
    	StringBuilder sbSelect2 = new StringBuilder();
    	sbSelect1.append("select "); 
    	sbSelect1.append("* "); 
    	sbSelect1.append("from MY_TABLE mytable"); 
    	sbSelect1.append("and mytable.myTimestamp= ? ");

    	String SQL = sbSelect1.toString();
    	try (Connection con = DriverManager.getConnection(connectionUrl); ) {
    		PreparedStatement stmt = con.prepareStatement(sbSelect1.toString());
    		
            ResultSet rs = stmt.executeQuery();

        
            Calendar cal 
            // Iterate through the data in the result set and display it.
            while (rs.next()) {
                System.out.print("Found Date: " + rs.getDate("myTimestamp"));
                System.out.print(" - Timestamp: " + rs.getTimestamp("myTimestamp"));
                System.out.print(" - Milis: " + rs.getTimestamp("myTimestamp").getTime());
                Calendar calResult = Calendar.getInstance();
                Timestamp ts = rs.getTimestamp("LastUpdTime", calResult);
                System.out.println(" - Calendar: " + ts);
            }
            
            PreparedStatement stmt = con.prepareStatement(sbSelect1.toString());
            
            
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }
}

{% endhighlight %}


# The solution
There're 2 ways to solve this issue
1. Change your compatibility level 
2. Change your column type to datefield2

The idea between these 2 strategies is that you change the compatibility level to support your old applications but once you are ready, you can go ahead and change the column type


[Spring JPA repostories]: https://docs.spring.io/spring-data/jpa/docs/1.5.0.RELEASE/reference/html/jpa.repositories.html
[Change your compatibility level]: https://docs.microsoft.com/en-us/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2016
[MSSQL 2016 datetime]https://docs.microsoft.com/en-us/sql/t-sql/data-types/datetime-transact-sql?view=sql-server-2016