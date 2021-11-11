---
layout: post
title: Quick review of Typescript basics
date: 2021-11-06 08:00:00:00 +0600
description: A quick review on typescript for angular
img: posts/default-post.jpg # Add image post (optional)
fig-caption: None
tags: [development, typescript]
---

## What's typescript
Typescript is very similar to javascript because it's an extension of javascript

 1. **Typescript cannot be used directly on the browser.** Typescript can be compiled to javascript but it cannot be used directly on the browser.
 
 You can install typescript by typing the following command. You can also check the latest at [typescriptlang.org] (https://www.typescriptlang.org/download)
 {% highlight shell %}
npm install typescript --save-dev
{% endhighlight %}

 2. **It uses static typing.** This means that unlike javascript where variables can change type or be created at any point in time. Typescript is more strict and it'll encourage you to declare your variables and use them according to the declared type.


While this is possible in javascript and it works like an overloaded function ( Numbers will add and strings will concatenate )

{% highlight javascript %}
 //Javascript
function add(a, b) {
    return a + b;
}

const result = add('2', '5')
{% endhighlight %}

With typescript you'd usually declare your types for safety:

{% highlight typescript%}

//Typescript
function add(a: number, b: number) {
    return a + b;
}

const result = add(2, 5);
{% endhighlight %}

 3. **it's compiled.** Unlike javascript which you can run directly on your browser (which makes it an interpreted language), typescript needs to be compiled before you run it.

 
## Types

### Primitives
 - number
{% highlight typescript%}
let myNumber: number;
myNumber = 20;
{% endhighlight %}
 - string
{% highlight typescript%}
 let myString: string;
myString = 'some string';
{% endhighlight %}
 
 - boolean
 
{% highlight typescript%}
 let myBoolean: boolean;
myBoolean = false;
{% endhighlight %}

### Complex types
 -  arrays
 
 {% highlight typescript%}
let myArray: string[];
myArray = ['S1', 's2'];
{% endhighlight %}


 - objects 
 
{% highlight typescript%}
 let myHouse: {
    type: string;
    myNumber: number;
};

myHouse = {
    type: 'classic',
    myNumber: 34
}
{% endhighlight %}

### Union types

This is to declare a variable that can hold more than one type.

{% highlight typescript%}
let myUnionType: string | number = 'test';

myUnionType = 4;
{% endhighlight %}

### Type aliases

This is the equivalent of structures in C, but it works like classes in javascript.

{% highlight typescript%}
type House = {
    type: string;
    houseNumber: number;
}

let mySecondHouse: House;
{% endhighlight %}

### Generics
Generics are very similar to java generics. It's a generic type used instead of a concrete type definition, this abstract type can be used around the function where it was declared.
It avoids working with repeated code while keeping it type safe.

{% highlight typescript%}
function myPush <T>(array: T[], value: T) {
    const newArray = [value, ...array];
    return newArray;
}
const demoArray = [1, 2, 3];

const updatedDemoArray = myPush(demoArray, -2);
{% endhighlight %}

### Classes
This is a class that very similar to other languages, it helps to define properties and operations of an object.
Typescript has constructors, which are very similar to C++.


{% highlight typescript%}
class DifferentHouse {
    type: string;
    size: number;

    constructor(type: string, size: number) {
        this.type = type;
        this.size = size;
    }

    grow(size: number) {
        this.size = size;
    }
}

const mansion = new DifferentHouse('Arch', 45);
mansion.grow(50);
{% endhighlight %}


### Class with constructor 

This is a class that uses a constructor to define the properties it contains.

{% highlight typescript%}
class ShortHouse {

    constructor(private type: string, private size: number) {
        this.type = type;
        this.size = size;
    }

    grow(size: number) {
        this.size = size;
    }
}

const mansion = new ShortHouse('Arch', 45);
mansion.grow(50);
{% endhighlight %}

### Interfaces
 - These are only available on typescript (not javascript).
 - They are very similar to *alias* with the main difference that they can be implemented by classes.
 - Ma


{% highlight typescript%}
//Declare an interface
interface House {
	size: number;
	model: string;
	
	build:() => boolean;

	
}

//Use an interface to declare an object
let myMansion: House;
myMansion = {
	size: 20,
	model: 'abcd1234'
};

//Use an interface to implement a class
class BigHouses implements House {
	size: number;
	model: string;
	build() {
		return true;
	}
}

{% endhighlight %}

### Initialize environment

In order to creat an intial configuration file, you can use the following command.
it creates a file called tsconfig.ts which contains the option to configure your typescript environment.

{% highlight shell %}
npx tsc --init
message TS6071: Successfully created a tsconfig.json file.
{% endhighlight %}