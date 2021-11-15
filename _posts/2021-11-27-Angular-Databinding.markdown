---
layout: post
title: Angular Databinding
date: 2021-11-27 08:00:00:00 +0600
description: Components configuration
img: posts/default-post.jpg # Add image post (optional)
fig-caption: None
tags: [development, angular]
---

## Databinding
it's linking our business logic (typescript) to our Template (html).

It can be **outbound**, from the business logic to the template.
 - *String interpolation:* {{ data }}
 - *Property binding:* [property] = "data"

or **inbound**, from the template to the business logic

 - *Event binding* (event) = "expression"
 
We can also have **two-way-binding**
 - [(ngModel)] = "data"
 

### String interpolation

From your *typescript*, you can directly map variables or methods that output a string  code to your *template*. 
The format to present data in the template using data binding is by surounding the *name* with double curly braces *{{myName}}*, this can print any string from the business logic to the UI.

{% highlight typescript%}
export class ServerComponent {
    serverName: string = "Ghost";
    serverStatus: string = "green";
    serverId: number = 10;

    getServerName() {
        return this.serverName; 
    }
}
{% endhighlight %}

{% highlight html%}
    {{'hardcoded String'}} <br>
    String: {{serverStatus}} <br>
    Number: {{serverId}} <br>
    A method: {{getServerName()}} <br>
{% endhighlight %}

### Property binding

This syntax is more suitable for scenario where you need to change values of html attributes. The format to use the value is different, you need to use variable name between square brackets.

{% highlight typescript%}
export class ServersComponent implements OnInit {

  allowNewserver = false;
}
{% endhighlight %}

{% highlight html%}
    <button class="btn btn-primary" [disabled] = "!allowNewserver">Add server</button>
{% endhighlight %}


## Event binding

Similar to *javascript*, you can also bind object events to your code, these events will execute when an event occours, for example onBlur, OnClick, etc. these are regular events for HTML tags.

{% highlight typescript%}
export class ServersComponent implements OnInit {

  allowNewserver = false;
  serverCreationStatus = "Nothing was added";
  constructor() {
    setTimeout(() =>  {
      this.allowNewserver = true;
    }, 2000);
   }

  ngOnInit(): void {
  }

  //My bound method
  onCreateServer() {
    this.serverCreationStatus = 'Server was added';
  }
}
{% endhighlight %}

{% highlight html%}
    <button class="btn btn-primary" 
	[disabled] = "!allowNewserver"
	(click)="onCreateServer()">Add server</button>
{% endhighlight %}


