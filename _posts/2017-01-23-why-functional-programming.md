---
layout: post
published: true
title: Why is functional programming important?
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

*Example 1*:
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

#### Functional example: Swift

```swift
let numbers = (1...20).filter{ $0 % 2 == 1}.map{ $0 * $0 }.map{ $0 - 1 }
numbers.forEach{ print($0) }
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

The above example was simple with no mutable states. Let's look a example with mutable state.

*Example 2*: Number classification

Natural numbers can be categorized into abundant, perfect and deficient. 
Perfect Number: Equals the sum of its positive divisors - Pair of numbers whose product yields the target number, excluding the number itself.

Sample 1: 6 is a perfect number because its divisors are 1, 2, 3 and 6 = 1+2+3; Similarly 28 = 1 + 2 + 4 + 7 + 14

|Classification|Condition |
|:--------------|:----------:|
| Perfect | Sum of factors = number |
| Abundant | Sum of factors > number |
| Deficient | Sum of factors < number |

#### Imperative Number classification

```java
import java.util.HashMap;
import java.util.HashSet;
import java.util.Map;
import java.util.Set;

public class ImpNumberClassifierSimple {

    private int _number;           //Internal state to hold the target number               
    private Map<Integer, Integer> _cache;   //Internal cache to prevent recalculation      

    public ImpNumberClassifierSimple(int targetNumber) {
      _number = targetNumber;
      _cache = new HashMap<>();
    }

    public boolean isFactor(int potential) {
      return _number % potential == 0;
    }

    public Set<Integer> getFactors() {
        Set<Integer> factors = new HashSet<>();
        factors.add(1);
        factors.add(_number);
        for (int i = 2; i < _number; i++)
            if (isFactor(i))
                factors.add(i);
        
        factors.stream().forEach(k-> System.out.println(k));
        System.out.println();

        return factors;
    }

    public int aliquotSum() {        //Calculation of aliquot sum, sum of factors - number itself              
        if (_cache.get(_number) == null) {
            int sum = 0;
            for (int i : getFactors())
                sum += i;
            _cache.put(_number, sum - _number);
        }
        return _cache.get(_number);
    }

    public boolean isPerfect() {
        return aliquotSum() == _number;
    }

    public boolean isAbundant() {
        return aliquotSum() > _number;
    }

    public boolean isDeficient() {
        return aliquotSum() < _number;
    }
    
    public static void main(String args[]) {
    	
    	ImpNumberClassifierSimple imp = new ImpNumberClassifierSimple(28);
    	System.out.println(imp.isPerfect());
    }
}
```

In ImpNumberClassifierSimple we have two elements of internal state. _number_ fields allows to us to avoid passing it as parameter to many functions. The _cache_ holds a map used to cache the sum for each number, yielding faster results. Internal state is common and encouraged in Object-oriented world because OOP languages utilize encapsulation as one of their benefits. Separating state often makes engineering practices such as unit testing easier, allowing easy injection of values.

---

#### Java 8 Number classification

```java
public class NumberClassifier {

    public static IntStream factorsOf(int number) {
        return range(1, number + 1)
                .filter(potential -> number % potential == 0);
    }

    public static int aliquotSum(int number) {
        return factorsOf(number).sum() - number;
    }

    public static boolean isPerfect(int number) {
        return aliquotSum(number) == number;
    }

    public static boolean isAbundant(int number) {
        return aliquotSum(number)> number;
    }

    public static boolean isDeficient(int number) {
        return aliquotSum(number) < number;
    }
    
    public static void main(String args[]) {
    	System.out.println("Is 28 perfect: " + NumberClassifier.isPerfect(28));
    }

}
```

---

The code in Java 8 version is dramatically shorter and simpler than in the original imperative version. All the methods are really self-contained, _pure functions_ with public, static scope. Because there is no internal state in the class, no reason to "hide" any of the methods. The _factors_ method is potentially useful in many other applications, such as searching prime numbers.

The finest-grained element of reuse in object-oriented systems is the class, and developers forget that resuse comes in smaller package. For example, the *sum* method accepts a Collection<Integer> rather than a specific type of list. That interface is general for all collections of numbers, making it more generally reusable at the function level.

In Java 8, the factorsOf() method returns a IntStream, allowing me to chain other operations onto it, including a terminating one that causes the stream to generate values. In other words, the return from factorsOf() isn't a list of integers but rather a stream that hasn't generated any values yet. Writing the aliquotSum() method is trivial; it is the sum of the list of factors minus the number itself. I wasn't required to write the sum() method - in Java 8, it is one of the stream terminators that generates values.

Streams in functional languages work more like potential energy, which is stored for later use. The stream holds the origin of the data, the origin comes from the range() method. The stream doesn't create the values until the developer "asks" for values, using a terminating operation such as _forEach()_ or _sum()_ . This is an example of _lazy evaluation_ .

---


### Conclusion

As you can see from above code, the code is elegant, simple and concise as convert our program from imperative to functional code. In functional programs methods filter, map nicely align with our requirement. In functional programs we are not dealing with temporary variables, variable mutations etc. Reading and maintaining this code is easy. In case requirements change it is relatively easy to change our functional code compared to imperative code. 

* Benefits of Functional programming
 1. Functional programs are easier to reason. One specific input will always give the same output.
 2. Functional programs are easy to test. Because there are no side effects, you don't need mocks.
 3. Functional programs are more modular because they're built from functions that have only input and output. 
 4. Functional programs makes composition and recombination much easier. 
 5. Functional programs are thread-safe as they avoid mutation of shared state. 


--- 

####  Features of functional programming languages

* Functional programming language features
 1. First-class functions
 2. Anonymous functions
 3. Closures
 4. Currying
 5. Lazy evaluation
 6. Parametric polymorphism
 7. Algebraic data types
 
---


### References

1. Functional programming in Java
2. Functionally Thinking
3. Functional programming in Swift
4. Functional Programming in Scala
