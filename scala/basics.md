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

---

# Option

- Represent a Value/Object or None
- Value/Object represented using an instance of Some
- null or non-existence values represented as None 

- Useful for handling null scenarios
- Avoid catching expressions by caller

---

# Option Example 1

```scala
def toInt(input: String): Option[Int] = {
    try {
      Some(input.toInt)
    } catch {
      case _: Throwable =>
        None
    }
  }
```

```scala
  toInt("100") match {
    case Some(i) => println(i)
    case None => println("Error!!")
  }
```

---

# Option Example 2
```scala
def toInt(input: String): Option[Int] = {
    try {
      Some(input.toInt)
    } catch {
      case _: Throwable =>
        None
    }
  }
```

```scala
var result: Option[Int] = toInt("100");
var result2: Option[Int] = toInt("test")
println("is empty", result.isEmpty);
println("get value ", result.get);
println("result2", result2.isEmpty);
println("getOrElse ", result.getOrElse(0));
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
case class CustomException(private val message: String = "", 
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
