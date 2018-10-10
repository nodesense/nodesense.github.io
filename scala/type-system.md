layout: true

.header[Scala Type System]
.footer[Gopalakrishnan Subramani @NodeSense <http://nodesense.ai>]
---

# Type System

.image-50![Default-aligned image](scala/assets/scala-type-system.png)

---


# References

- http://chariotsolutions.com/wp-content/uploads/2016/04/HeatherMiller.pdf

# Coverage

- Scala’s basic pre-defined types
- Defining your own types
- Parameterized types
- Bounds
- Variance
- Abstract types
- Type classes 

---

# Pre-Defined Type

.image[![type system](scala/assets/scala-type-system.png)]

---

# Unit 

Unit is a type that has exactly one value ‒ see Unit type, represents ()
A function that doesn't return anything must have the return type Unit. 


---

# Nothing

Nothing has no possible value - it is a Bottom type.
If it were Nothing then the function could not return a result. The only way to exit the function would be by an exception.

- Nothing is a subtype of every other type (including Null).
- There exist no instances of this type.

```scala
object None extends Option[Nothing]
```

```scala
object Nil extends List[Nothing]
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

# Defining own types?

1. Declarations of named types

e.g., traits or classes
Define a type member using the type keyword

```scala
class Animal(age:	Int)	{
		//	fields	and	methods	here...
}
trait Collection	{
		type	T
}
```

---

# Two ways to define types

1. Declarations of named types
    e.g., traits or classes
    Define a type member using the type keyword

2. Combine. Express types (not named) by combining existing types.
e.g., compound type, refined type

```scala
def cloneAndReset(obj:	Cloneable with	Resetable):	Cloneable	=	{	
		//...
}
```

---

# Parameterized Types

Interacting with typechecking via
Same as generic types in Java. A generic type is a generic class or interface that is parameterized over types. What are they?

```scala
class Stack[T]	{
  var elems: List[T]	=	Nil
  def push(x: T) { elems	=	x	::	elems	}
  def top:	T	=	elems.head
  def pop()	{	elems	=	elems.tail	}
  def isEmpty = elems.isEmpty
}
```

---

# Parameterized Type Example

```scala
class Stack[T]	{
  var elems: List[T]	=	Nil
  def push(x: T) { elems	=	x	::	elems	}
  def top:	T	=	elems.head
  def pop()	{	elems	=	elems.tail	}
  def isEmpty = elems.isEmpty
}

case class Bicycle(id: String);
```

```scala
val stack: Stack[Bicycle] = new Stack;
stack.push(Bicycle("cycle1"))
stack.push(Bicycle("cycle2"))
println (stack.top)
stack.pop()
println (stack.top)
stack.pop()
println(stack.isEmpty)
```

---

# Bounds

Parameterized types; we can constrain types.
Type Bounds are restrictions on Type Parameters or Type Variable. By using Type Bounds, we can define the limits of a Type Variable.
Both type parameters and type members
can have type bounds:

- Lower bounds (subtype bounds)
- Upper bounds (supertype restrictions)

---

# Upper Bound

.image-50[![type system](scala/assets/scala-upper-bound.png)]


T is a Type Parameter and S is a type. By declaring Upper Bound like “[T <: S]” means this Type Parameter T must be either same as S or Sub-Type of S.

---

# Upper Bound

```scala
class Animal
class Dog extends Animal
class Puppy extends Dog

class AnimalCarer{
  def display [T <: Dog](t: T){
    println(t)
  }
}

val animal = new Animal
val dog = new Dog
val puppy = new Puppy

val animalCarer = new AnimalCarer

//animalCarer.display(animal)
animalCarer.display(dog)
animalCarer.display(puppy)
```

---

#  Bound Example

```scala
trait Box[T	<:	Tool]
```

Example Lower Bound

```scala
trait Generic[T >: Null] {
    // `null` allowed due to lower bound
    private var	fld:	T	=	null
}
```

---

# Remember the type hierarchy?

All types have an upper bound of Any
and a lower bound of Nothing

.image-80[![type system](scala/assets/scala-type-system.png)]

---

# Bounds ?

```scala
trait Box[T	<:	Tool]
```

A Box can contain any element T which is a subtype of Tool

---

# Bounds ?

```scala
trait Generic[T >: Null] {
    // `null` allowed due to lower bound
    private var	fld:	T	=	null
}
```

Null can be used as a bottom type for any value that is nullable.
Recall class Null from the type hierarchy. It is the type of the null reference; it is a subclass of every reference class (i.e., every class that itself inherits from AnyRef)

- Note: Null is not compatible with value types

---

# Lower Bound

.image-50[![type system](scala/assets/scala-lower-bound.png)]

Here T is a Type Parameter and S is a type. By declaring Lower Bound like “[T >: S]” means this Type Parameter T must be either same as S or Super-Type of S.

---

# Lower Bound Example

```scala
class  Animal
class Dog extends Animal
class Puppy extends Animal

class AnimalCarer {
  def display [T >: Puppy](t: T){
    println(t)
  }
}

val animal = new Animal
val dog = new Dog
val puppy = new Puppy

val animalCarer = new AnimalCarer

animalCarer.display(animal)
animalCarer.display(puppy)
animalCarer.display(dog)
```

---

# Lower and Upper Bound Combining

One can also combine lower and upper bounds, as in T >: S <: U
- Where as T is the type whose bounds you are defining
- S is the lower bound 
- U is the upper bound. 
- T must come first (syntax), not in the middle.

---

# Lower and Upper Bound Example

```scala
 trait Thing
 class Vehicle extends Thing
 class Car extends Vehicle
 class Jeep extends Car
 class Coupe extends Car
 class Motorcycle extends Vehicle
 class Bicycle extends Vehicle
 class Tricycle extends Bicycle
```

Limit Parking to all the subtypes of Vehicles

```scala
 class Parking[A >: Jeep <: Vehicle](val plaza: A)
```

Can we limit Parking to all the subtypes of Vehicles, above Tricycle?

```scala
class Parking[A >: Bicycle <: Vehicle](val plaza: A)
```

---

# Variance?

Given the following:

```scala
trait Box[T]
class Tool
class Hammer	extends Tool
```

How might they relate to one another? Three possibilities:

- Covariant
- Contravariant
- Invariant

---

# Variance

.image[![type system](scala/assets/variance-types.png)]

---

# Reading

- https://apiumhub.com/tech-blog-barcelona/scala-type-bounds/

---