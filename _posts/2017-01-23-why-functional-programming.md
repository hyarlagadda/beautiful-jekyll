---
layout: post
published: false
title: Why is fuunctional programming important?
subtitle: Write quality, concise code using Functional programming. Imperative vs Functional programming. 
date: '2017-01-23'
---

![Why functional programming](/img/BlackBoard.png) 

## What is functional programming?


In general terms functional programming is a programming paradigm, and it’s about programming about functions. The tricky part is learning to think in a different (functional) way. Language doesn’t matter. Languages keep changing all the time. You could write functional programs in your current language. 

	Below is a quote by John Hughes in 1990 in the article “Why functional Programming matters”.

	1. No assignment statements: Functional programs contain no assignment statements, so variables, once given a value, never change. 
	2. No side effects: Generally functional programs contain no side effects at all. A function call can have no effect other than to compute its result. This eliminates a major source of bugs and also makes the order of execution irrelevant — since no side effect can change an expression’s value, it can be evaluated at any time. This relieves the programmer of the burden of prescribing the flow of control.
	3. Referentially transparent: Since expressions can be evaluated at any time, one can freely replace variables by their values and vice versa — that is programs are “referentially transparent”

--- 


### Imperative programming

Imperative program specify “How to do something”. Functional programs only care about “What needs to be done”. Imperative programs are modeled as sequence of commands that modify state. 

*Example*: 
Let’s illustrate the difference between Imperative and functional programming by example. For numbers 1 to 20, find odd numbers, square them and subtract one 1

#### Imperative example: Java

```java

public class ImperativeJava {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		int i = 1;
		List<Integer> numbers = new ArrayList<Integer>();
		
		while (i <= 20) {
			
			int k = i;
			//Odd number
			if (k % 2 == 1) {
				
				//square the number
				k = k * k;
				k = k - 1;
				numbers.add(k);
			}
			
			i++;
		}
		
		for (int k : numbers) {
			
			System.out.println(k);
		}
	}
	
}

```
  
---
 
#### Functional example: Java 8

```java

import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

public class FunctionalJava8 {

	public static void main(String[] args) {

		List<Integer> numbers = IntStream.range(1, 20).boxed()
         .collect(Collectors.toList());
		
		List<Integer> newList = numbers.stream().filter(k ->  (k % 2) == 1 )
			.map(k -> k * k).map(k -> k - 1).collect(Collectors.toList());
		
		newList.forEach(k -> System.out.println(k));
	}

}

```

---

#### Functional example: Scala 

```scala

object Functional extends App {
 
    val result = (1 to 20).filter( _ % 2 == 1).map( k => k * k ).map(_ - 1)
    result.foreach( println _ )
}

```
--- 	

#### Functional programming

More concepts

### Conclusion

### References
