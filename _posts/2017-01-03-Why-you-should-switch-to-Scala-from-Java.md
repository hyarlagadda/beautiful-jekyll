---
layout: post
published: true
title: Why Java developers should consider Scala
subtitle: Are you a seasoned Java developer and bored of Java
date: '2017-01-03'
---

![Happy New Year](/img/2016JumpTo2017Export.png) 

##    Happy New Year 2017 !!! 
    
If you are like me, you are a veteran Java developer for more than a decade. You are bored of writing boiler plate Java code year after year. The only Java changes you heard in a decade are Java version changes every four years or so. 
    
If you have been to Hackathons or Startupweekends, you have seen Ruby on Rails developers, AngularJS developers, Python developers hack away building full stack web apps in couple of hours. In contrast, as a Java developer you are still trying to create the folder structure for a traditional Java/J2EE application. How do you compete when your core skillset, Java in a JVM environment is such a big disadvantage? 
 
### New Kid on the block

#### You have a new language to the rescue. Welcome to Scala language !!!

Scala is a functional programming language built to run on Java JVM. That's right Scala needs Java JDK to run. Martin Odersky created scala after realizing all the downfalls of Java. In fact, Martin was original member of Java compiler team. Scala has no boilerplate code compared to Java.
        
* Scala has no boiler plate code.
* Writing concurrent/multithreaded code is a breeze
* [Type inference](#Type-Inference-Immutability)
* [Encourages immutability](#Type-Inference-Immutability)
* Strong Type safety
* [Simple class definition](#Getter-Setter-Not-Required). Getter and Setter methods on member data is not requied
* Large open source community ([PlayFramework](http://www.playframework.com) for web apps with scaffolding, [Akka](http://akka.io) for REST API, [Scalajs](https://www.scala-js.org/) for Javascript etc)
* Ability to write Domain Specific languages (DSL) with ease
* Runs on well known Java JVM environment
* Strong support of Testing (Unit testing frameworks - ScalaTest)
* Pattern matching (not regular expressions)
* Forget NullPointerExceptions as Option's will make your code safe
* You can reuse your existing Java libraries from Scala
* [Higher order functions](#Higher-Order-functions)

To try some of these samples [download](http://scala-ide.org/) Eclipse IDE for Scala. 

#### Java version

```java
package com.harishblog;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class SquareOfNumberCalculator {
 
  public static void main(String[] args) {
   
      List<Integer> myList = Arrays.asList(1, 2, 3, 4, 5);
      SquareOfNumberCalculator calculator = new SquareOfNumberCalculator();
      List<Integer> squaredNumbers = calculator.squareOfNumbers(myList);

      //Print original list
      System.out.println("Printing original numbers");
      calculator.printNumbers(myList);
      //Print squared list
      System.out.println("Printing squared numbers");
      calculator.printNumbers(squaredNumbers);
  }
	
   public void printNumbers(List<Integer> numbers) {
      
      for (Integer i : numbers) {
         System.out.println(" i --> " + i);
      }
   }

   public List<Integer> squareOfNumbers(List<Integer> numbers) {
       
       List<Integer> squaredNumbers = new ArrayList<Integer>();
       for (Integer i : numbers ) {
           squaredNumbers.add(i * i);
       }
       
       return squaredNumbers; 
    }

}
```

#### Scala version

```scala
package main.scala


object SquareOfNumberScalaCalculator extends App {

      //Create a list. No need of New 
      val list = List(1, 2, 3, 4, 5)
    
      println("Printing original list")
      list.foreach ( println ( _ ) )
    
      //Square every element in the list by calling map method on list
      val squaredList = list.map( x => x * x)
      println("Printing squared list")
      squaredList.foreach ( println _ )
      
      //Assign a function to a variable 
      //Both take input of type Int and return a Int
      val square: Int => Int = (x: Int) =>  x * x
      val cube = (x: Int) => x * x * x
      val newSquare = (x: Double) => x * x
      
      //Function that takes a list and function as parameter
      //The function name is "operation" of type Int input and Int output
      def operateOnList(list: List[Int], operation: (Int) => Int): List[Int] = {
        list.map(operation(_))
      }
     
      //square 
      val squareList = operateOnList(list, square)
      
      //Cube
      val cubeList = operateOnList(list, cube)
      
      //Below code will not work as method signature for newSquare ( (Double) => Double) 
      //doesn't match expected (Int) => Int
      //val squareOfDoubles = operateOnList(list, newSquare)
      
      println("Squared list \n")
      squareList.foreach( println _ )
      println("Cubed list \n")
      cubeList.foreach( println _ )
      
      //filter. Filter operation with function literal
      //val cubeGT15 = cubeList.filter( (x) => x > 15)
      
      //Simplified function literal
      val cubeGT15 = cubeList.filter( _ > 15)
      
      println("Cubes > 15")
      cubeGT15.foreach( println _ )
     
      //Define a class
      case class Person(firstName: String, lastName: String)

      //Instantiate a class
      val obama = Person("Barack", "Obama")
      println("first Name: " + obama.firstName)
      println("last Name: " + obama.lastName)
      
      val trump = Person("Donald", "Trump")
      val bush = Person("George", "W Bush")
      val clinton = Person("Bill", "Clinton")

      //Create a list
      val presidents = List(trump, obama, bush, clinton)
      
      //Find the presidents with first names starting with B. Creates a new immutable list
      val presidentsWithFirstNameB = presidents.filter( _.firstName.startsWith("B"))
      
      //Print first names
      presidentsWithFirstNameB.foreach(x => println(x.firstName))
}
```
The first line

**object SquareOfNumberScalaCalculator extends App {**

Keyword **_object_** makes this a Singleton. The **_extends App_** makes all the code within like a main method in Java.

**_listToPrint.foreach(println( _ ))_**

We are passing a funtion **_println_** to a function **_foreach_**. This is called functional programming or Higher Order functions. **_foreach_** executes any function you pass to it on every element of the collection. In this case println( _ ). The **_ _ _** (underscore) is current element. 

----


### Type Inference and Immutability


<a name="Type-Inference-Immutability">

 **_val list = List(1, 2, 3, 4, 5)_**
 
 In scala during initialization we can define variable to be a variable (var) or a constant (val). Scala prefers Immutability whenever possible. So you can't reassign variable list to any thing else as it is a val. There is no need for **_new_** for creating List. We will discuss that later. In Scala data types are inferred. You never mentioned constant list is of type List collection but Scala compiler will infer it. 
 
 **_val squaredList = list.map( x => x * x)_**
 
 We are calling a map method on list. A map operation on a collection executes function passed on every element of the collection and returns another **_NEW_** collection. Here, we are passing a anonymous function **_x => x * x_** It takes each element and multiplies by itself (square).
 
**_val square = (x: Int) =>  x * x_**

Assign a function that takes Input input and Int return to variable square. Similary for cube.

---- 


### Higher Order functions


<a name="Higher-Order-functions"></a>

```scala
val square: Int => Int = (x: Int) =>  x * x
```

We assigned a function to a variable square. square is a type of function signature ( Int => Int ) that takes input as Int and returns a Int. The body of the function is **_(x: Int) => x * x_**

```scala
val cube = (x: Int) => x * x * x
```

We assigned a variable cube to a function. The function type here is inferred ( Int => Int ) instead of explicity specifying it. The body of function is **_(x: Int) => x * x * x_**

**_def operateOnList(list: List[Int], operation: (Int) => Int): List[Int] = {_**

**_def_** is keyword for defining a function. It takes parameter list of type **_List[Int]_** . The return type is **_List[Int]_**. In scala you don't need return statement. The last statement in a function is the return value.

Define a function "operateOnList" that takes a list and function as parameters. The signature of function parameter is Input input and Input output. Any function that satisfies this signature can be passed. Both square and cube constant vals satisfy this condition.



---- 


<a name="Getter-Setter-Not-Required"></a>


### Simple class definition 

**_case class Person(firstName: String, lastName: String)_**

Here we defined a class with member variables, constructor, getter and setter methods.
 
---- 

### Companies using Scala

You might be wondering, nobody at work uses Scala why should I learn it. Below, are some top tech companies large and small using Scala.
   
* Twitter
* LinkedIn
* Foursquare
* Netflix
* AirBnB
* The Guardian
* Apple
* Precog
* Sony
* Workday
* Precog
* Workday

----

#### Conclusion
 
 Think about all the boiler plate code we had to write in Java for squaring a number (For loop and all). Also, you don't need semicolons for every statement. Types are inferred. Anonymous functions make it easy to express developer intentions. 
 
 We haven't even scratched the surface of Scala. This is a gentle introduction to get your feet wet. 
 
 Cheers to a New Year and learning a new language Scala !!!
 
 


