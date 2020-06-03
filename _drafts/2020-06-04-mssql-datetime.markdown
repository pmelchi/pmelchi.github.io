---
layout: post
title: MS SQL 2016 datetime issue with java
date: 2020-06-03 08:00:00:00 +0600
description: MSSQL 2016 and above issue with java and datetime # Add post description (optional)
img: 2020-06-04-mssql.jpg # Add image post (optional)
fig-caption: MSQSQL 2016# Add figcaption (optional)
tags: [java, hibernate, mssql2016, datetime, datetime2]
---


In this post I'll describe the troubleshooting steps that worked for me in order to figure out and solve an issue with java and MS SQL server 2016

I was making some changes to an old java application, this application uses Spring JPA repostories which helps you to handle your DB mapping
It has some convenient features but the one in interest here is "save", which conveniently figures out for you if you are trying to INSERT or UPDATE your entity

You don't even need to have code, the example below implementes "save" just by extending JpaRepository

{% highlight java %}
@Transactional(readOnly = true) 
public interface CustomerRepository extends JpaRepository<Customer, Long> {

  Page<Customer> findByLastname(String lastname, Pageable pageable); 
}
{% endhighlight %}

This code was working perfectly fine in another environment but in this environment in particular we were receiving an error when trying to update some rows

Let's assume the following code 
{% highlight java %}


{% endhighlight %}



[Spring JPA repostories]: https://docs.spring.io/spring-data/jpa/docs/1.5.0.RELEASE/reference/html/jpa.repositories.html