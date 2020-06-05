---
layout: post
title: MSSQL and Java timestamp issue 
date: 2020-06-03 08:00:00:00 +0600
description: MSSQL 2016 and above have issue with java and datetime
img: 2020-06-04-mssql.jpg # Add image post (optional)
fig-caption: MSQSQL 2016# Add figcaption (optional)
tags: [java, hibernate, mssql2016, datetime, datetime2]
---

#The issue
##I cannot query by timestamp in MSSQL 2016
The issue itself is that making queries to a MSSQL 2016 database will break if you are using a timestamp, the problem is that starting in MSSQL 2016 datetime has changed to provided more accuracy 

This can be easily seen in the following query:

{% highlight java %}
select cast (SYSDATETIME ( ) as datetime) as my_datetime,  cast (SYSDATETIME ( ) as datetime2) as my_datetime2
{% endhighlight %}

| my_datetime             | my_datetime2                |
|-------------------------|-----------------------------|
| 2020-06-05 14:05:07.123 | 2020-06-05 14:05:07.1224577 |


You can notice how *datetime* includes only 3 digits in the millisecond field while *datetime2* includes 7, so is 123 equal to 1224577? Not according to MSSQL
My personal thinking is that MSSQL should be smart enough to know and cast accordingly but according to the documentation the problem comes because java has only 1 SQL field type for timestamp (java.sql.Timestamp), 
so they decided to upgrade the field type without a warning (I mean you could have kept this between JDBC versions) 

They upgrade itself is mentioned in t


#My Issue 
I was making some changes to an old java application, this application uses Spring JPA repostories which has some convenient features but the one in interest here is "save", 
which figure out for you if you are trying to INSERT or UPDATE your entity by using only 1 method (Although this is not the only way to implement this behavior, this is the way it was implemented for this application)

{% highlight java %}
@Transactional(readOnly = true) 
public interface CustomerRepository extends JpaRepository<Customer, Long> {

  Page<Customer> findByLastname(String lastname, Pageable pageable); 
}
{% endhighlight %}

I made a couple changes and this code was working perfectly fine in one of my environments but it was failing in a second environment (Classic developer complaining becuase it works fine in his computer - Everyone) 


#The solution
There're 2 ways to solve this issue
1. Change your compatibility level 
2. Change your column type to datefield2

The idea between these 2 strategies is that you change the compatibility level to support your old applications but once you are ready, you can go ahead and change the column type


[Spring JPA repostories]: https://docs.spring.io/spring-data/jpa/docs/1.5.0.RELEASE/reference/html/jpa.repositories.html
[Change your compatibility level]: https://docs.microsoft.com/en-us/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2016