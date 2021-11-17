---
layout: post
title: Angular directives
date: 2021-12-04 08:00:00:00 +0600
description: How to use angular directives
img: posts/default-post.jpg # Add image post (optional)
fig-caption: None
tags: [development, angular, directives]
---

## Directives
Directives are a kind of HTML extension in angular, that give the ability to provide additional functionality to our tags.
 
(Additional information)[https://angular.io/guide/built-in-directives]

### Structural directives

Directives that change the DOM layout by adding and removing DOM elements.

#### NgIf and else

Adding a template conditionally with else

{% highlight html%}
    <p *ngIf="myBooleanAttribute; else noServer"> Server was added: {{serverName}}</p>
	<ng-template #noSuccess>
		<p> Nothing yet</p>
	</ng-template>
{% endhighlight %}

### Attribue directives

Directives that change the appearance or behavior of an element, component, or another directive.

## NgStyle

Adds and removes a set of HTML styles.



{% highlight html%}
    <p [ngStyle]="{backgroundClor: getColor()}" > </p>
{% endhighlight %}