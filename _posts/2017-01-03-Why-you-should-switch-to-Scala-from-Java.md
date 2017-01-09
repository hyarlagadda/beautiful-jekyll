---
layout: post
published: true
title: Why Java developers should consider Scala
subtitle: Are you a seasoned Java developer and bored of Java
date: '2017-01-03'
---

![ScalaVSJava](/img/ScalaVSJava.png)

##    Happy New Year 2017 !!! 
    
If you are like me, you are a veteran Java developer for more than a decade. You are bored of writing boiler plate Java code year after year. The only Java changes you heard in a decade are Java version changes every four years or so. 
    
    
If you have been to Hackathons or Startupweekends, you have seen Ruby on Rails developers, AngularJS developers, Python developers hack away building full stack web apps in couple of hours. In contrast, as a Java developer you are still trying to create the folder structure for a traditional Java/J2EE application. How do you compete when your core skillset, Java in a JVM environment is such a big disadvantage? 
 
### New Kid on the block

#### You have a new language to the rescue. Welcome to Scala language !!!

Scala is a functional programming language built to run on Java JVM. That's right Scala needs Java JDK to run. Martin Odersky created scala after realizing all the downfalls of Java. In fact, Martin was original member of Java compiler team. Scala has no boilerplate code compared to Java.
        
* Scala has no boiler plate code

* To try some of these samples [download](http://scala-ide.org/) Eclipse IDE for Scala. 

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
  
     //Define a function to print elements in list    
     def printList(listToPrint: List[Int]): Unit = {
       
       //Call foreach method on each element of list
        listToPrint.foreach(println( _ ))
      }
        
      //Create a list
      val list = List(1, 2, 3, 4, 5)
    
      println("Printing original list")
      printList(list)
    
      //Square every element in the list by calling map method on list
      val squaredList = list.map( x => x * x)
      println("Priting squared list")
      printList(squaredList)
}
```
The first line

**object SquareOfNumberScalaCalculator extends App {**

Keyword **_object_** makes this a Singleton class. The **_extends App_** makes all the code within like a main method in Java.

**def printList(listToPrint: List[Int]): Unit = {**

**_def_** is keyword for defining a function. It takes parameter listToPrint of type **_List[Int]_**. The return type is **_Unit_** aka void in Java.

**_listToPrint.foreach(println( _ ))_**

We are passing a funtion **_println_** to a function **_foreach_**. This is called functional programming or Higher Order functions. **_foreach_** executes any function you pass to it on every element of the collection. In this case println( _ ). The **_ _ _** (underscore) is current element. 

 **_val list = List(1, 2, 3, 4, 5)_**
 
 In scala during initialization we can define variable to be a variable (var) or a constant (val). Scala prefers Immutability whenever possible. So you can't reassign variable list to any thing else as it is a val. There is no need for **_new_** for creating List. We will discuss that later.
 
 **_val squaredList = list.map( x => x * x)_**
 
 We are calling a map method on list. A map operation on a collection executes function passed on every element of the collection and returns another collection. Here, we are passing a anonymous function **_x => x * x_** It takes each element and multiplies by itself (square).

#### Conclusion
 
 Think about all the boiler plate code we had to write in Java for squaring a number (For loop and all). Also, you don't need semicolons for every statement. Anonymous functions make it easy to express developer intentions.
 
 We haven't even scratched the surface of Scala. This is a gentle introduction to get your feet wet. 
 


