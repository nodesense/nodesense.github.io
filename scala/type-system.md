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
- Existential types
- Type classes 

---

# Pre-Defined Type

.image[![type system](scala/assets/scala-type-system.png)]

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

Parameterized types; you can constrain them.
Both type parameters and type members
can have type bounds:

- Lower bounds (subtype bounds)
- Upper bounds (supertype restrictions)

Example

```scala
trait Box[T	<:	Tool]
```

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

.image-50 [![type system](scala/assets/scala-type-system.png)]

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

