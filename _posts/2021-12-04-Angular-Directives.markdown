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

#### NgStyle

Adds and removes a set of HTML styles.

We are adding  the directive between square brackets *[directive]* because we need to link the behavior to the attribute. 
This is usually linked to a method.

{% highlight html%}
    <p [ngStyle]="{backgroundClor: getColor()}" > </p>
{% endhighlight %}


In the example above, we are linking the css attribute directly, but we can also set a list of styles and return it as a *record*

{% highlight typescript%}
    currentStyles: Record<string, string> = {};

	setCurrentStyles() {
	  // CSS styles: set per current state of component properties
	  this.currentStyles = {
		'font-style':  this.canSave      ? 'italic' : 'normal',
		'font-weight': !this.isUnchanged ? 'bold'   : 'normal',
		'font-size':   this.isSpecial    ? '24px'   : '12px'
	  };
	}
{% endhighlight %}


(More information) [https://angular.io/guide/built-in-directives#ngstyle]

#### NgClass
Adds and removes a set of CSS classes.
This is similar to the one above but it changes CSS classes instead. This is usually a conditional expression.

{% highlight html%}
    <p [ngClass]="{greenSucces: myAttribute === 'success'}" > </p>
{% endhighlight %}

(More information)[https://angular.io/guide/built-in-directives#ngClass]