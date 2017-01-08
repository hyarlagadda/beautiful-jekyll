---
layout: post
published: true
title: Why Java developers should consider Scala
subtitle: You been a Java developer for a while and you are bored
date: '2017-01-03'
---
##    Happy New Year 2017 !!! 
    
If you are like me, you are a veteran Java developer for more than a decade. You are bored of writing boiler plate Java code year after year. The only Java changes you heard in a decade are Java version changes every four years or so. 
    
    
If you have been to hackactons or Startupweekends, you can see Ruby on Rails developers, AngularJS developers hack away building full stack web apps in couple of hours. In contrast as a Java developer you are still trying to create the folder structure for a traditional Java/J2EE application. How do you compete when your core skillset, Java in a JVM environment is such a big disadvantage? 
 
### New Kid on the block

#### You have a new language to the rescue. Welcome to Scala language !!!

Scala is a functional programming language built to run on Java JVM. That's right Scala needs Java JDK to run. Martin Odersky created scala after realizing all the downfalls of Java. In fact, Martin was original member of Java compiler team. Scala has no boilerplate code compared to Java.
        
* Scala has no boiler plate code

* To try some of these samples download Eclipse IDE for Scala. 

### Java version


 {% highlight java linenos %} 

package com.harishblog;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
public class SquareOfNumberCalculator {
public static void main(String[] args) {
// TODO Auto-generated method stub
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
{% endhighlight %}
