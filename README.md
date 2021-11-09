# The Weird Part of Javascript

## Chapter-4 Object & Function 

Object & Dot
 - Object can have primitive property 
 - Object can contain another object (this will consider as object property)
 - object can also contain function

 ```js
 var person = {
     name:'Mir', // <======== primitive type
     address:{state:'50 west malibag',zipCode:'1217'},// <=== object type
     getName:function(){ // <==== function type
         console.log(this.name)
     }
 }
 ```

 Accessing object property 
  - Property of an object can be access using the `computed member access operator '[]'`.
  
  ```js
    var person = new Object()
    person['firstName'] = 'Mir' //<==== This create a property 'firstName' inside the person object

    // To access the value from an object
    // we can assign the property in a variable
    var propertyName = 'firstName'

    console.log(person[propertyName]) //<=== This will return 'Mir', Under the hood javascript run the code like person.'firstName' but this is not an acceptable syntax
  ```

Child Object
- we can create a child inside an object

```js
    var person = new Object()
    person.name = 'Mir'
    person.address = new Object() //<=== this will create a child object inside  the person object
    person.address.state = 'BD'
```

Accessing the child property
- to access the property of a child object we can do the following

```js
    console.log(person['address']['state']) // <==== this will return 'BD'
```
Object Literals
 - Object literals are more faster than creating an object using the `new` keyword

 ```js
    var person = {} // syntax for object literals
 ```

 JSON and Object literals 
 - In the old days data were send using xml notation

 ```xml
 <object>
    <firstName>Mir</firstName>
 </object>
 ```
 As we can see we have to use redundant code just to send one line of string

 To reduce this bandwidth loss currently data are send using JSON 

 ```js
    {"firstName":"Mir"} // this is also a valid object literal syntax
 ```
- JSON is a subset of javascript object
- In javascript we can create object on the fly i.e

```js
    function greet({name:'Mir'}){
        console.log('Hi ' + name)
    }
```

Faking NameSpace

 - What is Namespace : A container for variable or function.Most language has namespace (eg:Java,C#),but in javascript has no namespace convention,but we can fake the namespace convention.

 ```js
  var greet = 'Hello'
  var greet = 'Hola' 
  console.log(greet) // return 'Hola'
 ```
 But if we want to import two function whose name are same then there will be a naming collision.To resolve this javascript use object to fake the namespace.

 ```js
    var english = {}
    var spanish = {}
    english.greet = 'Hello' // both greet can be a function,primitive or object
    spanish.greet = 'Hola'

    // function
    //page name mir.js
    function greet(){
        console.log('hi mir')
    }
    //page name sahib.js
    function greet(){
        console.log('hi mir')
    }

    //importing greet ,this is very concise import

    var mir = {}
    var sahib = {}
    mir.greet = greet()
    sahib.greet = greet()

 ```
Note: faking namespace has the power to import two file which contain function that have the same name

Pass by value & Pass by reference
 - Pass by Value: In pass by value scenario the memory location of an primitive type is copied to the new memory location and that new memory location is assign to the variable

```js
    var a = 3 // memory location is assign to var a
    var b; // var b is undefined 
    b = a // a new memory location is created and value 3 is copied to that location and that location is assigned to b
    a = 2 // var a is assign to new memory location which contain value 2
    console.log(b) // return 3 cause primitive type are pass by value
```

 - Pass by reference: In Javascript object is passed by reference which mean when it create an object in memory and that object is assign to another variable.The memory location of that object is assigned to the variable.

 ```js
    var a = {name:'Mir'}
    var b;
    b = a
    a.name = 'Sahib'
    console.log(b) // return name:Sahib
 ```

 Function and Object

 - In javascript function are treated like variable which mean we can assign function to a variable,pass a function as parameter or create function on the fly(defination of first class function).
- In javascript function reside in memory as special type of object which has special property.
- In javascript we attach the following thing with a function
  1.  primitive type
  2.  object
  3.  another function

- In javascript function has two hidden property
  1. Name (function can have a name or not,function without a name are called anonymous function)
  2. Code (body of the function which is invocable)

  ```js
  function greet(){
      console.log('hi')
  }

  greet.language = 'English' // attaching a primitive type string into the function greet
  greet.getLanguage = function(){
      console.log(this.language)
  }
  greet.person = {name:'Mir'}
  
  console.log(greet.language) // return 'English'
  console.log(greet.getLanguage()) // return 'English'
  console.log(greet.person.name) // return 'Mir'
  ```
Function statement & function expression
- In javascript statement does the action/work and expression return a value

```js
    a = 3 // js express return a memory location to variable a
    3+1 // code in the memory is executen and return to the console

    if(a===3){ // js statement,doesn't return any value 
        //do something
    }
```
- In simple word statement doesn't return any value 

- Since function is an object, we can use function as statement and also as an expression

Function Statement
```js
// this is is function statement 
// it reside in memory and don't return anything unless it get executed
    function greet(){
        console.log('hi')
    }
```
- function statement can be hoisted because it already reside in the memory

```js
    greet() // hoisting, function is called before it was define
    function greet(){
        console.log('hi')
    }
```

Function expression
```js
    var anonymousGreet = function(){
        console.log('hi')
    }
```
- In the code above a memory is allocated when the function is defined and that memory location is return to the anonymous variable (the memory location is return using the `=` operator, `=` is a special function).Thus proving that function can be defined as express.
- To invoke the code part of the function we can do

```js
var anonymousGreet = function(){
        console.log('hi')
    }
    anonymousGreet()// invoking the code part of the function
```

- function can be created on the fly 

```js
    function log(a){ // function pass as parameter
        a() // function is invoked 
    }

    log(function(){ // function is created on the flu
        console.log('Hi')
    })
```
