---           
layout: post
title: Object Oriented Programming in JavaScript with DCS
date: 2012-08-16 14:05:37 UTC
updated: 2012-08-16 14:05:37 UTC
comments: true
sharing: true
categories: [ javascript ] 
tags: [ javascript, OOP ]
---

In the process of learning JavaScript there always comes a point when you really want to implement
Object Oriented Programming in a very easy way. There are lots of libraries to accomplish this task,
and they are really straightforward. But sometimes you really need something even simpler or maybe 
you want to implement it yourself so that you really understand the concepts behind it, and this 
was my case; I wanted to implement a very simple class system so that I could understand more about 
how JavaScript prototype system works and how to emulate inheritance in a very simple way.

After surfing the web a bit I run in to John Resig's [blog post](http://ejohn.org/blog/simple-javascript-inheritance/) 
in which he explains how to implement OO programming in JavaScript in an easy and clean way. So after
reading it I decided to implement my own class system, just for fun, and called it _**Dummy Class System**_ or _**DCS**_

DCS is a very simple/dummy class system for JavaScript. DCS lets you implement Object Oriented
Programming with ease. As I mentioned before DCS is influenced by the simple JavaScript inheritance
mechanism implemented by John Resig and is also a bit influenced by the class system defined by [Ext JS](http://www.sencha.com/products/extjs/)

Here is an example of what you can do with DCS:

Define the Class **Person**

<pre class="prettyprint" data-lang="javascript">
    DCS.define('Person', { 
        property: { 
            name: '', 
            lastname: '' 
        }, 

        constructor: function(name, lastname) { 
            this.name = name; 
            this.lastname = lastname; 
        }, 

        toString: function() { 
            return 'Name: ' + this.name + ' Lastname: ' + this.lastname; 
        } 
    }); 
</pre>

The config object (the second parameter of the _DCS.define_ method) contains the methods and properties
that will be part of the new class prototype, except for the **_property_** config object that you
can use to specify default values for instance variables. The **_property_** config also tells DCS to 
generate getters/setters for each instance variable specified in this object. Therefore you can use 
these generated methods as usual: 

<pre class="prettyprint" data-lang="javascript">
    // create a new instance of Person
    var p1 = new Person("John", "Doe");
    console.log(p1.getName());      // prints "John"
    console.log(p1.setName("foo")); // sets the name to "foo"
    console.log(p1.getName());      // prints "foo"
</pre>

Define the Class **Worker** which extends from Person

<pre class="prettyprint" data-lang="javascript">
    DCS.define('Worker', { 
        extend: 'Person', 

        property: { 
            jobTitle: '' 
        }, 

        constructor: function(name, lastname, jobTitle) { 
            this._super(name, lastname); 
            this.jobTitle = jobTitle; 
        }, 

        toString: function() { 
            return this._super() + ' Job Title: ' + this.jobTitle; 
        } 
    });
</pre>

One thing to notice here is that you can still have access to an overriden method by using 
the **__\_super__** reference, this reference have temporary access to its parent's overriden method. 
As you can see is quite simple to do OO programming with DCS. 

For more information about the project visit the source code repository at [github](https://github.com/jorgeramirez/dcs).  
Feel free to download and play with it.
