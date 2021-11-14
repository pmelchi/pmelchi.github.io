---
layout: post
title: Component configuration
date: 2021-11-13 08:00:00:00 +0600
description: Components configuration
img: posts/default-post.jpg # Add image post (optional)
fig-caption: None
tags: [development, angular]
---

Inside our component, the typescript file (.ts)  contains 3 basic elements that help us with the configuration.

 - selector
 - template
 - styles

{% highlight typescript%}
@Component({
  selector: 'app-testa',
  templateUrl: './testa.component.html',
  styleUrls: ['./testa.component.css']
})

{% endhighlight %}
 

## Selector
It usually starts with the word app and it's the name that will help us identify and use our component across the application. This is very similar to CCS selectors where we can select elements by tag, attribute or class.

### As an element tag

This allows us to insert the whole component as an element in the web page.
 
 {% highlight typescript%}
import { Component } from "@angular/core";

@Component({
    selector: 'app-server', // Select as a tag
    templateUrl: './server.component.html'
})
export class ServerComponent {

}
{% endhighlight %}
 
 {% highlight html%}
<app-server></app-server>
{% endhighlight %}

### As an element attribute

This allows to use the component inside other tags.
 
  {% highlight typescript%}
import { Component } from "@angular/core";

@Component({
    selector: '[app-server]', // Select as a attribute
    templateUrl: './server.component.html'
})
export class ServerComponent {

}
{% endhighlight %}
 
 {% highlight html%}
<div app-servers></div>

{% endhighlight %}

### As an element class

This allows to use the component inside other tags.
 
{% highlight typescript%}
import { Component } from "@angular/core";

@Component({
    selector: '.app-server', // Select as a class
    templateUrl: './server.component.html'
})
export class ServerComponent {

}
{% endhighlight %}
 
 {% highlight html%}
<div class="app-servers"></div>
{% endhighlight %}

## Template

Template has 2 different ways to use it:

### By pointing to an HTML file
This is the default when you create a component via CLI.

{% highlight typescript%}
@Component({
  selector: 'app-testa',
  templateUrl: './testa.component.html',//Pointing to html file
  styleUrls: ['./testa.component.css']
})
{% endhighlight %}

### By adding the template to your code
This is useful in scenarios where it's very snippet, like in a single tag scenario.

{% highlight typescript%}
@Component({
  selector: 'app-servers',
  template: `<app-server></app-server>
  <app-server></app-server>`,
  styleUrls: ['./servers.component.css']
})
{% endhighlight %}

## Styles

You have 2 main options here too 
 - External file
 - Snippet 
 
There're also special selectors, which you can find in the [angular reference page](https://angular.io/guide/component-styles)
 
### Pointing to an external file

This is an array and it allows you to add multiple styles.

{% highlight typescript%}
@Component({
  selector: 'app-testa',
  templateUrl: './testa.component.html',
  styleUrls: ['./testa.component.css', '../main.css']
})
{% endhighlight %}

### Adding it as a snippet

We add the CCS directly to our component code, usually in a single string.

{% highlight typescript%}
@Component({
  selector: 'app-root',
  template: `
    <h1>Tour of Heroes</h1>
    <app-hero-main [hero]="hero"></app-hero-main>
  `,
  styles: ['h1 { font-weight: normal; }']
})
export class HeroAppComponent {
/* . . . */
}
{% endhighlight %}