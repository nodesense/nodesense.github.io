layout: true

.header[Scala Basics, Expressions]
.footer[Scala]
---

# Scala

- Scalable Language
- High-level language for the JVM
- Object oriented + functional programming
- Statically typed
- Designed by Martin Odersky

---

# Scala

- Runs on Java Virtual Machine

- Comparable in speed to Java*
- Type inference, Smart Compiler, knows types from expressions
- Interoperates with Java
    - Can use any Java class (inherit from, etc.)
    - Can be called from Java code

---

# Scala


- Expressive
- First-class functions
- Closures - Encapsulation in Functional world
- Concise - Smaller code
- Type inference 
- Literal syntax for function creation
- Java interoperability
- Can reuse java libraries
- Can reuse java tools
- No performance penalty

---

# Scala

- Compiles to java bytecode
- Works with any standard JVM
- Or even some non-standard JVMs like Dalvik
- Scala compiler written by author of Java compiler

---

# Use Cases

- Data Analytics
- Machine Learning
- Concurrent Programming
- Tasks
- Big Data Streaming

---

# Popular Frameworks build on Scala

- Apache Spark
- Apache Kafka
- Akka Framework
- Kafka Framework
- Play Framework

---

# Example Code

Declaring variables:

```scala
var x: Int = 7
var x = 7 // type inferred
val y = “hi” // read-only
```

Functions

```scala
def square(x: Int): Int = x*x

def square(x: Int): Int = {
            x*x
}

def announce(text: String) =
{
 println(text)
}
```

---

# Compile

- Scala compiled to Java byte-code
- Produces .class files
- JVM compatible
---

# Scala REPL

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
- No binary compatibilities

---

# Type checking

- Strongly Typed Language
- Compile Time and Runtime type checking

---

# Scala 2.12 Features 

- Uses Java 8 
- Scala Trait compiled to Java Interface ()
- Functions can be called from both direction easily
- Java Lambda and FunctionN are now Single Abstract Method

# Scala 2.13 Features

- Compiler Performance (10 to 20 % more)
- Deprecating procedural functions syntax (towards Scala 3.0)
- Collection Simplification (towards Scala 3.0)

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

# Expressions

Most of the statements in Java are expressions in Scala
Expressions returns output. Statement doesn't.

- if is an expression
- for..yield is an expression
- match..case is an expression

---

# If Expression

```scala
// below statement returns 10

if (true) 10

//below statement returns 20

if (false) 10 else 20

// assign to result
val result = if (false) 10 else 20
println(result);
```

---

# If Expression

- else if

```scala
if (a > b)
       if (c)
          100
       else
          50
     else 10
```

# if with block statement

- multi line statements

```scala
if (a > b) {
      if (c) {
        100
      }
      else {
        50
      }
    }
    else {
      10
    }
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

---


# Exceptions

- Scala Support exception handling
- keywords, try, catch, finally
- keywords: throws, throw

```scala
def div(a:Int,b:Int):Float={
    a/b
}
// will  throw java.lang.ArithmeticException
div(1, 0)
```

---

# Catch Exceptions

```scala
def div(a:Int,b:Int):Float={
    try{
        a/b
    }catch{
        case e:ArithmeticException=> {
            println(e)
            0 // return value
            }
    }
}

div(10, 2) // 5.0
div(10, 0) // throw error, catched, return 0
```

---

# Catch Generic Exception

- throw keyword rethrow the exception

```scala
def getValue(list: List[Int], index:Int): Int = {
     try{
         list(index)
     }catch{
        case e:ArithmeticException=> {
            println(e)
            throw e
        }
        case anon:Throwable=> {
                println("Unknown exception: "+anon)
                throw anon
        }
     }
}

getValue(List(10,20), 0) // returns 10
// throw java.lang.IndexOutOfBoundsException
// catched and rethrow the exception
getValue(List(10,20), 100) 
```

---

# Exception finally block

```scala
def div(a:Int,b:Int):Float={
    try{
        a/b
    }catch{
        case e:ArithmeticException=> {
            println(e)
            0 // return value
            }
    }
    finally {
        println("I am always called")
    }
}
```

---

# Exception throw generic exception

```scala
def vote(age:Int) = {
     if(age<18) 
        throw new Exception("Sorry, you're ineligible yet")
     else  println("Cast your vote now")
}

vote(12) // throws Exception
vote(18) // doesn't throw
```

---

# Checked Exceptions
 
- Checked exception like Java style

```scala
@throws(classOf[Exception])  
def vote(age:Int) = {
     if(age<18) 
        throw new Exception("Sorry, you're ineligible yet")
     else  println("Cast your vote now")
}
```

---

# Custom Exception with Case Class

```scala
case class CustomException(
        private val message: String = "", 
        private val cause: Throwable = None.orNull) extends 
                                    Exception(message, cause)
```

```scala
try {
    throw CustomException("Yeah, exception")
} catch {
    case c: CustomException =>
          c.printStackTrace
}
```

---

# Custom Exception with Class

- exception with overloaded auxiliary constructor 

```scala
class CustomException(message: String) extends Exception(message) {

  def this(message: String, cause: Throwable) {
    this(message)
    initCause(cause)
  }

  def this(cause: Throwable) {
    this(Option(cause).map(_.toString).orNull, cause)
  }

  def this() {
    this(null: String)
  }
}
```

```scala
throw new CustomException()
throw new CustomException("bad here")
```

---

# import a package

- Import classes, objects from other packages

```scala
import scala.util

var rnd = new util.Random
println(rnd.nextInt())
```

---

# import a class/object

- Import classes, objects from other packages

```scala
import scala.util.Random

var rnd = new Random
println(rnd.nextInt(1000))
```

---

# import all

- use specific classes/objects

```scala
import scala.util.{Random, Success}

var rnd = new Random
println(rnd.nextInt(1000))
```

---

# import all

- use _ for importing all

```scala
import scala.util._

var rnd = new Random
println(rnd.nextInt(1000))
```

---

# import a class/object

- Import with alias name

```scala
import scala.util.{Random => RandomX}

var rnd = new RandomX
println(rnd.nextInt(1000))
```

---

# import Hide

- Hide random, import everything
- Random is not imported

```scala
import scala.util.{Random => _, _}

//below lines throw error
var rnd = new Random
println(rnd.nextInt(1000))
```

---

# import scope

- import in scope bountry, 
-- Random can't be accessed outside scope

```scala
def generateRandom : Int = {
    import scala.util.{Random}

    var rnd = new Random
    var n = rnd.nextInt()
    return n;
}
```

---

# Compile Scala Code

    scalac <filename.scala>

now we have filename.class produced

To de-compile generated byte code to Java

    javap filename 

or 
    javap filename.class

---

# Parse Scala source code

To know, how Scala transpile Scala

    scalac -Xprint:parse Main.scala

    scalac -Xprint:all Main.scala
