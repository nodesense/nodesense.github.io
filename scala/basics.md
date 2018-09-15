layout: true

.header[Scala Basics, Expressions]
.footer[Gopalakrishnan Subramani @NodeSense <http://nodesense.ai>]
---


# Scala

- Objected Oriented and Functional Language
- Runs on Java Virtual Machine
- Java Interoperablity
- Designed by Martin Odersky
---

# Use Cases

- Data Analytics
- Machine Learning
- Concurrent Programming
- Tasks
- Big Data Streaming
---

# Popular Frameworks

- Apache Spark
- Apache Kafka
- Akka Framework
- Play Framework
---

# Compile

- Scala compiled to Java byte-code
- Produces .class files
- JVM compatible
---

# Scala Interpretter

- Download Scala lang
- Set path to scala/bin to PATH
- Run scala in terminal/command prompt

```
scala > println("hello")
```
---

# Scala Advantages

- Reduce Code size Approx 1-2 times compared to Java
- Type Inference [Drive data type automatically*]
- Smart Compiler
- Can use all Java libraries
---

# Scala Cons

- Steep Learning curve
- Overloaded signs, symbols
- Slightly painful to use inside Java
- Compiler bugs
- No binary compatiblities
---

# Strongly Typed

- Strongly Typed Language
- Compile Time and Runtime type checking

---

# Scala Operators

- Java Operators are functions
- Operator overloading supported

---

# Operators

- Arithmetic +, \-, *, %, / 
- Logical &&, ||, !
- Relational >, <, >=, <=, !=, ==
- bitwise &, |
- Assignment =, +=, -=

---

# Operators

- No ++ self increment
- No -- self decrement

---

# Ternary

- There is no ternary operator
- Use if else in place

```scala
val a = if (i % 2 == 0) "even" else "odd"
```
---

# Data Types

- Boolean (true/false)
- Byte, Short (16 bits), Int (32 bits), Long (64 bits)
- Float (32 bits), Double (64 bits)
- Char (16 bits), Unicode
- String
- Data Types are class types
---

# Variables

- Mutable variable (__var__)
- Immutable values (__val__)

```scala
val PI: Float = 3.14.toFloat;
//ERROR
PI = 2.14;
```
---

# Immutable

- Values can't be changed once assigned
- Useful in functional programming
- Library immutable collection
- Threadsafe by nature

```scala
val PI: Double = 3.14;
//ERROR
PI = 2.14;
```

---

# For loop over list iteration

List are iteratable
```scala
    var numList = List(1, 2, 3, 4, 5, 6);
    for ( x <- numList) {
        println(x)
    }
```
prints
    1, 2, 3, 4, 5, 6

---

# For Nested loop

Nested loops can be flatted into single line
```scala
    for ( i: Int <- 1 to 3; j: Int <- 4 to 6) {
	    println(i, j)
	}
```
prints 

	(1, 4), (1, 5), (1, 6)
	(2, 4), (2, 5), (2, 6)
	(3, 4), (3, 5), (3, 6)


---

# For To

Scala has variances of for loop
The simple one
```scala
    for ( i: Int <- 0 to 5) {
	    println(i)
	}
```
this prints 0, 1, 2, 3, 4, 5


---

# For Until
```scala
    for ( i: Int <- 0 until 5) {
	    println(i)
	}
```

prints 0, 1, 2, 3, 4


---

# For loop with if 
Adding conditions
```scala
    var numList = List(1, 2, 3, 4, 5, 6);
    for ( x <- numList if x %2 == 0) {
        println(x)
    }
```
prints
    2, 4, 6
---

# For Yield

Using yield gets the iteratable
```scala
    var itr = for (i <- 0 until 5) yield i;
    
    for (k <- itr) {
     println(k);
    }
```
---

#For Loop with break
Must include breakable, from 'Breaks' package
```scala
    import util.control.Breaks._
    ......
    breakable {
        for (i <- 1 to 10) {
        if (i == 5)  break;
            println(i);
        }
    }
```
---

# For Loop with Continue

- No direct support for continue
- Use break inside loop
- Below loops print only odd number

```scala
import util.control.Breaks._;

for (i <- 1 to 10) {
    breakable {
        if (i % 2 == 0)  break;        
        println(i);
    }
}
```