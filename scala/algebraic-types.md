layout: true

.header[Algebraic Types]
.footer[Scala]
---

# Algebra

- A set of objects
- The operations that can be applied to those objects to create new objects
- _Numeric algebra_ 
   1. A set of objects, such as whole numbers
   2. The operations that can be used on those objects: +, -, * (and /)
- _Relational Algebra_
   1. Relational DB, for example, a set of database records in table,  select, update, join queries,  called as operations that creates new type as output  

---

# Algebraic Data Types

Three main categories

- Sum type
- Product type
- Hybrid types

---

# Sum Type

- The Sum type is also referred to as an “enumerated type”
- Enumerate all of the possible instances of the type.

```scala
sealed trait Direction
case object North extends Direction
case object South extends Direction
case object East extends Direction
case object West extends Direction
```

How many possible object for Direction? Answer 4.

---

# Sum Type

- Sum types are typically created with a sealed trait as the base type, with instances created as case objects.
- The number of enumerated types you list are the only possible instances of the base type
- Define Sum type with “is a” and “or”. For example, North is a type of Direction, and Direction is a North or a South or an East or a West

```scala
sealed trait Bool
case object True extends Bool
case object False extends Bool
```

How many possible object for Type Bool? 2 

---

# Sum Type

- How many values of type Nothing?

- How many values of type Unit?

- How many values of type Boolean?

- How many values of type Byte?

- How many values of type String?

---

# Sum type

- How many values of type Nothing? → 0

- How many values of type Unit? → 1

- How many values of type Boolean? → 2

- How many values of type Byte? → 256

- How many values of type String? → many

---

# Sum type with OR 

- How many values of type Byte or Boolean?

- How many values of type Boolean or Unit?

- How many values of type (Byte, Boolean) or Boolean?

- How many values of type Boolean or (String, Nothing)?

---

# Sum Type with OR

- How many of type Byte or Boolean? → 2 + 256 = 258

- How many of type Boolean or Unit? → 2 + 1 = 3

- How many of type (Byte, Boolean) or Boolean? → (256 × 2) + 2 = 514

- How many of type Boolean or (String, Nothing)? → 2 + (many × 0) = 2

---

# Sum Type and Tuple

- How many values of type (Byte, Boolean)?

- How many values of type (Byte, Unit)?

- How many values of type (Byte, Byte)?

- How many values of type (Byte, Boolean, Boolean)?

- How many values of type (Boolean, String, Nothing)?

---

# Sum Type and Tuple

- How many of type (Byte, Boolean)? → 2 × 256 = 512

- How many of type (Byte, Unit)? → 256 × 1 = 256

- How many of type (Byte, Byte)? → 256 × 256 = 65536

- How many of type (Byte, Boolean, Boolean)? → 256 × 2 × 2 = 1024

- How many of type (Boolean, String, Nothing)? → 2 × many × 0 = 0

---

# Sum types! This or That

```scala
Nothing = 0
Unit    = 1
Boolean = 2
Byte    = 256

(Unit , Boolean) = 1 × 2 = 2 
 Unit | Boolean  = 1 + 2 = 3 // not Scala syntax

(Byte , Boolean) = 256 × 2 = 512
 Byte | Boolean  = 256 + 2 = 258

(Boolean, Boolean, Boolean, Boolean, 
 Boolean, Boolean, Boolean, Boolean) = 256

// sums all the way down
Boolean = true | false
Int = 1 | 2 | 3 | ...
```

---

# Sum type

```scala
sealed trait Pet
case class Cat(name: String) extends Pet
case class Fish(name: String, color: String) extends Pet
case class Squid(name: String, age: Int) extends Pet

val bob: Pet = Cat("Bob")
```

```scala
def sayHi(p: Pet): String = 
  p match {
    case Cat(n)      => "Meow " + n + "!"
    case Fish(n, _)  => "Hello fishy " + n + "."    
    case Squid(n, _) => "Hi " + n + "."    
  }
```

```scala
sayHi(Cat("Bob")) // match to Cat(n)
```
---

# Sum Type Exhaustiveness Checking

```scala
def sayHi(p: Pet): String = 
  p match {
    case Cat(n)      => "Meow " + n + "!"
    case Fish(n, _)  => "Hello fishy " + n + "."    
  }
```

Compiler warning

<console>:17: warning: match may not be exhaustive.
<pre>
It would fail on the following input: Squid(_, _)
         p match {
         ^
</pre>

---

# Sum Type: Option

```scala
sealed trait Option[+A] 
case object None extends Option[Nothing]
case class  Some[A](a: A) extends Option[A]
```

```scala
def safeDiv(a: Int, b: Int): Option[Int] =
  if (b != 0) Some(a / b) else None

```

scala> val x = safeDiv(10, 2)
x: Option[Int] = Some(5)

scala> val y = safeDiv(10, 0)
y: Option[Int] = None

---


# Sum Type: Either

```scala
sealed trait Either[+A, +B] 
case class Left[A](a: A)  extends Either[A, Nothing]
case class Right[B](b: B) extends Either[Nothing, B
```

```scala
def safeDiv(a: Int, b: Int): Either[String, Int] =
  if (b != 0) Right(a / b) else Left("Divide by zero!")

scala> val x = safeDiv(10, 2)
x: Either[String,Int] = Right(5)

scala> val x = safeDiv(10, 0)
x: Either[String,Int] = Left(Divide by zero!)
```

---

# Sum Type Try 

```scala
sealed trait Try[+A]
case class Success[A](a: A) extends Try[A]
case class Failure[A](t: Throwable) extends Try[A]
```

```scala
import util._ // it's scala.util.Try

def safeDiv(a: Int, b: Int): Try[Int] =
  Try(a / b)

scala> val x = safeDiv(10, 2)
x: scala.util.Try[Int] = Success(5)

scala> val x = safeDiv(10, 0)
x: scala.util.Try[Int] = Failure(java.lang.ArithmeticException: / by zero)
```

---

# List Example

```scala
sealed trait List[+A]
case object Nil extends List[Nothing]
case class ::[A](head: A, tail: List[A]) extends List[A]

object List {
  def apply[A](as: A*): List[A] = ...
}
```

```scala
def sum(ns: List[Int]): Int =
  ns match {
    case Nil     => 0
    case n :: ns => n + sum(ns)
  }

scala> sum(List(1,2,3))
res23: Int = 6
```

---

# The Product type This and That

- Scala case class constructor to create a data type whose number of possible concrete instances can be determined by multiplying the number of possibilities of all of its constructor fields

```scala
type Person = (String, Int)
```

```scala
class ScalaPerson(val name: String, val age: Int)
```

---

# Hybrid types

- An algebraic data type is any data that uses the two patterns (Sum and Product).

---


# References

- https://alvinalexander.com/scala/fp-book/algebraic-data-types-adts-in-scala
- http://tpolecat.github.io/presentations/algebraic_types.html
