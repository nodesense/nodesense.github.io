layout: true

.header[Scala Functions Basics]
.footer[Gopalakrishnan Subramani @NodeSense <http://nodesense.ai>]
---

# Functions

---

# Pure Function

1. The function always evaluates to the same result value given the
same argument value(s). It cannot depend on any hidden state or
value, and it cannot depend on any I/O.
2. Evaluation of the result does not cause any semantically observable
side effect or output, such as mutation of mutable objects or output
to I/O devices.

---

# Advantage of writing pure functions?

Pure functions respect the immutablity, no hidden state or global state
or thread or local variable influence the result.

- Easier to combine/chain with other function
- Easier to test
- Easy  to debug
- Idempotent
- Referential transparency
- Memoizable
- Lazy

---

# Function Multiple Args

A function can accept variable number of arguments by using * in the declaration

```
def sumAll(name: String, args:Int*) : Int  =  {
      var count: Int = 0
      for {arg: Int <- args}
      count += arg;
      count
}
```

> sumAll("add")

prints 0

> sumAll("add", 10, 20, 30)

print 60

---

# Function

### Below function sums number between range a and b recursively
```scala
def sum(a: Int, b: Int): Int {
    if (a > b) 0 else a + sum(a + b, b)
}
```

Call it like,

> sum(1, 5)

prints 15

---

# assign function

 below statement throws exception, that wraps the function sum

```scala
> var sum2 = sum

sum2: (Int, Int) => Int = $$Lambda$1149/2135841337@33de7f3d

but we can convert to lambda
below code retuns the lambda

> var sum2 = sum _

> sum2(1, 5)

returns 15


> var sum3 = sum (_, _)

returns 
sum3: (Int, Int) => Int = $$Lambda$1157/407958234@38d42ab7

> sum3(1, 5)

returns 15

When we assign function to variable, it automatically converts to lambda

Now defined a funciton square,
> def square(a: Int): Int= a * a

> Higher order function that square numbers and sum a to b

```
def sumSquare(f: Int => Int, a: Int, b: Int): Int{ 
    if (a > b) 0 else f(a) + sumSquare(f, a+1, b)
}
```


> sumSquare(square, 1, 5)
res27: Int = 55


# Function Multiple Args

A function can accept variable number of arguments by using * in the declaration

```
def sumAll(name: String, args:Int*) : Int  =  {
      var count: Int = 0
      for {arg: Int <- args}
      count += arg;
      count
}
```

> sumAll("add")

prints 0

> sumAll("add", 10, 20, 30)

print 60

# Function

### Below function sums number between range a and b recursively
```
def sum(a: Int, b: Int): Int {
    if (a > b) 0 else a + sum(a + b, b)
}
```

Call it like,

> sum(1, 5)

prints 15

## assign function
 below statement throws exception, that wraps the function sum

> var sum2 = sum

sum2: (Int, Int) => Int = $$Lambda$1149/2135841337@33de7f3d

but we can convert to lambda
below code retuns the lambda

> var sum2 = sum _

> sum2(1, 5)

returns 15


> var sum3 = sum (_, _)

returns 
sum3: (Int, Int) => Int = $$Lambda$1157/407958234@38d42ab7

> sum3(1, 5)

returns 15

When we assign function to variable, it automatically converts to lambda

Now defined a funciton square,
> def square(a: Int): Int= a * a

> Higher order function that square numbers and sum a to b

```
def sumSquare(f: Int => Int, a: Int, b: Int): Int{ 
    if (a > b) 0 else f(a) + sumSquare(f, a+1, b)
}
```


> sumSquare(square, 1, 5)
res27: Int = 55

# Default values

def printName(firstName:String = "Unknown") {
  println(firstName)
}

printName()


# Named arguments

```scala
def printName(firstName:String, lastName:String) {
    println(firstName, lastName)
}

printName(firstName="Krish", lastName="S")
printName( lastName="S", firstName="Krish")
```


## Call-by-Name: => Type

The => Type notation stands for call-by-name, which is one of the many ways parameters can be passed. If you aren't familiar with them, I recommend taking some time to read that wikipedia article, even though nowadays it is mostly call-by-value and call-by-reference.

What it means is that what is passed is substituted for the value name inside the function. For example, take this function:

```scala
def f(x: => Int) = x * x
If I call it like this

var y = 0
f { y += 1; y }
```
Then the code will execute like this

```scala
{ y += 1; y } * { y += 1; y }
```

Though that raises the point of what happens if there's a identifier name clash. In traditional call-by-name, a mechanism called capture-avoiding substitution takes place to avoid name clashes. In Scala, however, this is implemented in another way with the same result -- identifier names inside the parameter can't refer to or shadow identifiers in the called function.

There are some other points related to call-by-name that I'll speak of after explaining the other two.

## 0-arity Functions: () => Type

The syntax () => Type stands for the type of a Function0. That is, a function which takes no parameters and returns something. This is equivalent to, say, calling the method size() -- it takes no parameters and returns a number.

It is interesting, however, that this syntax is very similar to the syntax for a anonymous function literal, which is the cause for some confusion. For example,

```
() => println("I'm an anonymous function")
```

is an anonymous function literal of arity 0, whose type is

```
() => Unit
```
So we could write:
```
val f: () => Unit = () => println("I'm an anonymous function")
```

It is important not to confuse the type with the value, however.

## Unit => Type

This is actually just a Function1, whose first parameter is of type Unit. Other ways to write it would be (Unit) => Type or Function1[Unit, Type]. The thing is... this is unlikely to ever be what one wants. The Unit type's main purpose is indicating a value one is not interested in, so doesn't make sense to receive that value.

Consider, for instance,

def f(x: Unit) = ...
What could one possibly do with x? It can only have a single value, so one need not receive it. One possible use would be chaining functions returning Unit:

val f = (x: Unit) => println("I'm f")
val g = (x: Unit) => println("I'm g")
val h = f andThen g
Because andThen is only defined on Function1, and the functions we are chaining are returning Unit, we had to define them as being of type Function1[Unit, Unit] to be able to chain them.

Sources of Confusion
The first source of confusion is thinking the similarity between type and literal that exists for 0-arity functions also exists for call-by-name. In other words, thinking that, because

() => { println("Hi!") }
is a literal for () => Unit, then

{ println("Hi!") }
would be a literal for => Unit. It is not. That is a block of code, not a literal.

Another source of confusion is that Unit type's value is written (), which looks like a 0-arity parameter list (but it is not).



# Partially Applied Functions

def plus(a: Int)(b: Int) = a + b

def plus2 = plus(2)(_)

or 

def plus2 = plus(2)_
dsa

def wrap(prefix: String)(html: String)(suffix: String) = {
prefix + html + suffix
}

val hello = "Hello, world"
val result = wrap("<div>")(hello)("</div>")

returns <div> Hello, world</div>

Alternative way,

val wrapWithDiv = wrap("<div>")(_: String)("</div>")

wrapWithDiv("<p>Hello, world</p>")

<div><p>Hello, world</p></div>

val wrapWithPre = wrap("<pre>")(_: String)("</pre>")

### Handling the missing parameter

It’s necessary to specify the type of the missing parameter, as I did in this
code:
val wrapWithDiv = wrap("<div>")(_: String)("</div>")

# Curried Functions

def add(x: Int, y: Int) = x + y

val addFunction = add _

addFunction was type of function2

addFunction: (Int, Int) => Int = <function2>

(add _).isInstanceOf[Function2[_, _, _]]

True


addFunction.isInstanceOf[Function2[_, _, _]]

Then they create a “curried” function from that Function2 instance:

val addCurried = (add _).curried

Now you can use the new curried function like this:

addCurried(1)(2)

Now create  create a partially-applied function from the curried function,
like this:

val addCurriedTwo = addCurried(2) // create a PAF
addCurriedTwo(10) // use the PAF


Partial function without parameter group

def wrap(prefix: String, html: String, suffix: String) = {
prefix + html + suffix
}

val wrapWithDiv = wrap("<div>", _: String, "</div>")

wrapWithDiv("Hello, world")

---

# identity function

identity is the identity function defined in predef package in Scala (given a value, it simply returns that same value) 

Below code converts List[Option[A]] into List[A] using flapMap.
Here o => o function is called identity function.

```scala
val l = List(Some("Hello"), None, Some("World"))
l.flatMap( o => o)
```

Scala has identity that does exactly same.  note, [Option[String]] is needed due to conversion to iteratable. 

```scala
l flatMap identity[Option[String]]
```

The same code can be written using for expression.

```scala
for(x <- l; y <- x) yield y
```

```scala
l.map(identity) == l 
// returns true
```

Scala 2.8 onwards, we have flatten method

```scala
l.flatten[String]
```