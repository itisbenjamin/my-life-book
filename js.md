# Javascript Basic Grammar"

I want to put these basic grammar all together here. To make things more convenient.

## JS Basics

*Computer* programs are lists of instructions. They are run linearly. 

*Code* is what computer programs are written in. 

*Grammar* is the foundation of language. Programming languages are built upon sets of tules called syntax. 

*Semicolons* is optional to be used, but is neccessary when having two statements on the same line. 

**Syntaxt**

Includes keywords like `var`, `return` and `true`. 

*Comments* are denoted by `//`. They are not read by the computer. 

**Variables**

Store data and are the building blocks of Javascript. 

Each variable is defined by a case-sensitive name.

{% highlight js %}
var myVariable = "data"
console.log(myVariable)
{% endhighlight %}

**String**

String can be sequences of characters. It can also include spaces, punctuation, and numbers. 

They are identified by double quotes. 

**Numbers**

There is no need to use quote when you value numbers. 

`var myNumber = 10`

**Expressions**

An expression can combine numbers, string and variables to output a value. They are evaluated from left to right when coding. 

**Arithmetic**

The four basic forms of arithmetic are represented by symbols called operators and are used when creating expressions.

{% highlight js %}
var myNumber = 10 + 2
console.log(myNumber)
{% endhighlight %}

The same as C grammar, they are `+`, `-`, `*`, `/` and `%`。

**Booleans**

Booleans can be used to store true or false outcomes.

{% highlight js %}
var myBooleans = true
console.log(myBooleans)
{% endhighlight %}

**Comparisons**

There are six kinds of way to compare data.

{% highlight js %}
> Greater than
< Less than
>= Greater than or equal to
<= Less than or equal to
!= Not equal to 
== Equal to
{% endhighlight %}

Booleans work closely with comparision operators and rely on them to determine whether the boolean will output a true or false value.

## Variables

Variables are containers for storing values and are essential to write complex computer programs.

**Delaration**

You can use `var` to declare a variable. 

**Naming**

A variable's name is unique and case-sensitive.   
You can put your variable's name after the keyword `var`. 

**Assignment**

To assign a value, you can use `=`. 

{% highlight js %}
var myName = "Ben"
console.log(myName)
{% endhighlight %}

**Reassignment**

Variables are containers for values and you can replace the existing value in a variable with a new value.

**Types**

Data types: number, string, boolean.   
Variables can store values of any data type.

{% highlight js %}
var myString = "String"
var myNumber = 33
var myBoolean = true
{% endhighlight %}

**Undefined**

The data type undefined denotes the absence of a value.  
If you declare a variable, but don't assign a value, it automatically holds the value undefined.

{% highlight js %}
var myNothing
console.log(myNothing)
{% endhighlight %}

Then the computher will output "undefined".

**Initialization**

When a variable is given a value it is called initialization. 

**Type Comparisons**

You can use `===` and `!==` to compare the value and data type. 

{% highlight js %}
var Something = 10 === "10"
console.log(Something)
{% endhighlight %}

Then the computer will output `false`. 

## Functions

Functions are the verbs of programming.  
They tell the computer to do a set of actions.   

{% highlight js %}
function myFunction(){
console.log("Function!")
}

myFunction()
{% endhighlight %}

**Console.log**

This funcion has the computer print data to the console for your viewing.

**Declaring Functions**

You can use the keyword `function` to declare a funcion and give is an action to execute inside `{}`.

**Storing Functions**

You can also use a variable to store function.   
This can make it more easier when we use a funcion.

{% highlight js %}
var myFunction = function(){
console.log("Funciont!")
}

myFunction()
{% endhighlight %}

**Parameters**

Parameters are variables you give a function as inputs inside `()`.  
Parameters are given specific values when you call the function. 

{% highlight js %}
var getCost = function(price){
console.log( "$" + price )
}

getCost(20)
{% endhighlight %}

Then the `price` is a parameter. 

**Calling Functions**

When you call a function you are assigning a value to your parameters.  
This value is called an argument.

**Arguments**

Arguments are the values you assign to parameters.

`20` is an argument.

**Missing Arguments**

If a function with a parameter is called with a missing argument, that parameter is assigned the value undefined by default.

{% highlight js %}
function say(myname){
  console.log(myname)
}

say()
{% endhighlight %}

**Body**

Anything inside `()` is considered the body of the function, and is executed when the function is called.

{% highlight js %}
function getcost(price){
  var tip = price * 0.2
  var cost = price + tip
console.log("$" + cost)
}

getcost(20)
{% endhighlight %}

****


