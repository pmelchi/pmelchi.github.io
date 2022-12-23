---
layout: post
title: Content projection
date: 2021-12-05 08:00:00:00 +0600
description: How to use Angular content projection
img: posts/default-post.jpg # Add image post (optional)
fig-caption: Default
tags: [development, angular, projection]
---

## Content projection

Content projetion is inserting content inside your component tag (in your template) and using it by projecting that content to another component.
You achive this by adding a *body* within your component tag and then using the *<ng-content>* to select where this content will be rendered.
 
(Content projection)[https://angular.io/guide/content-projection]

There are 3 common implementations for this:

 - Single-slot content projection
 - Multi-slot content projection
 - Conditional content projection

### Single-slot content projection

Select where to put the content via *ng-content*
{% highlight html%}
<h2>Single-slot content projection</h2>
    <ng-content></ng-content>
{% endhighlight %}

Add the content between the component selector tags.
{% highlight html%}
<app-zippy-basic>
  <p>Is content projection cool?</p>
</app-zippy-basic>
{% endhighlight %}

### Multi-slot content projection

This is achived by using a selector which will work as a type of *switch* logic where specific content will go to the css selector and everything else can go to the default.

Two slots:
 - Selector specific .
 - Default with everything else.

{% highlight html%}
<h2>Multi-slot content projection</h2>

    Default:
    <ng-content></ng-content>

    Question:
    <ng-content select="[question]"></ng-content>
{% endhighlight %}

{% highlight html%}
<app-zippy-multislot>
  <p question>
    Is content projection cool?
  </p>
  <p>Let's learn about content projection!</p>
</app-zippy-multislot>
{% endhighlight %}


### Conditional content projection

When we want our content to be for example redered based on a condition or multiple times, then we need to use *ng-template*. The main difference is that in with this element, the content won't be rendered until is needed (with *ng-content* the content is already there even when not used)

This usually requires:

 1. A way to render the content, like: *ngTemplateOutlet*
 2. The source sorounded by *ng-template*