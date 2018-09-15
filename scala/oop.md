layout: true

.header[Scala Object Oriented]
.footer[Gopalakrishnan Subramani @NodeSense <http://nodesense.ai>]
---

# Class

- Scala support classes
- Encapsulation, inheritance, polymorphism
- Single Inheritance
- Polymorphism
- Classes can have instance variable, methods, properties
- Java style getter/setters (get/set)

---

## Access Specifier
- public [default, no specific keyword]
- _private_
- _protected_

---

## Constructor

- One Primary constructor
- Multiple Auxiliary constroctors
- this for access current class members
- super for base class

---

## Constructor Primary

- Primary constructor defined in class definition
- Params in constructor become member variable by default

```scala
class Appliance(var name: String, var price: Int) {
}

var a = new Appliance("Light", 100);
println(a.name, a.price)
```
---

# Constructor Member, Access Specifier

- Constructor can have member definition
- Below example, name, price are members
- price is private instance variable

```scala
class Appliance(var name: String, private var price: Int) {
}

var a = new Appliance("Light", 100);
println(a.name)
```

---


# Auxiliary Constructor

- Secondary constructors
- defined with __this__ keyword inside class
- Auxiliary constructor must start with call to previous constructor/default constructor

```scala
//# Auxiliary Constructor
class Appliance {
    private var name = "";
    private var price = 0;

    def this(name: String) {
        this(); //calls default
        this.name = name;
    }
    ....
}

new Appliance()
new Appliance("TV")
```

---


# Auxiliary Constructor Contd
 
```scala
//# Auxiliary Constructor
class Appliance {
    private var name = "";
    private var price = 0;
    ....
    def this(name: String, price: Int) {
        this(name); //previous cons
        this.price = price;
    }
}
...
new Appliance("TV", 20000)
```

---


# Access specifier

- Public, by default 
- No __public__ keyword
- __private__ keyword for inside class access
- __protected__ keyword for child classes

```scala
class Counter {
    private var count = 0;

    // public method
    def increment() { count += 1; }

    // this class and child class
    protected def current() = count
}

val counter = new Counter
counter.increment();
```

---

# Getter and Setter

- Getter, Setter similar to Java 
- def to define get property 
- def with suffix _ for setter
- Not compatible with Java (get/set)Name pattern

---

# Getter and Setter

```scala
class Appliance {
    private var itemPrice = 0
    //public getter
    def price = itemPrice
    //public setter (propery name with _)
    // note NO SPACE between _=
    def price_= (newPrice: Int) {
        if (newPrice >= 0)
            itemPrice = newPrice
    }
}

let appliance = new Appliance()
println(appliance.price) //calls getter
appliance.price = 100 //calls setter
appiance.price = 0 // calls setter, but do not set value
```

---

# Java compatible getter/setters

- per JavaBean specification
- to use @BeanProperty

```scala
import scala.reflect.BeanProperty

class Applicance {
    @BeanProperty var name: String = _
}

// Generate 4 methods automatically

// scala compatible
name: String
name_ = (newValue: String) :Unit

// java compatible
getName() : String
setName(newValue: String) : Unit
```

---

# Inheritance

- Scala support inheritance
- Uses __extends__ keyword
- __override__ to override base class methods
- __super__ to call base class cons/methods 

---

# Inheritance

```scala
class Appliance(var name: String) {
}

class Light(name: String) extends Applicance(name) {
}

class Fan(name: String) extends Applicance(name) {
}

var d = new Fan("Fan1")
println(d.name)
```

---

# Object Casting asInstanceOf

```scala
class Appliance {}
class Light extends Appliance {}
var appliance:Appliance = new Light;

//doesn't work, downward casting
//var light:Light = appliance;

//right way
var light:Light = appliance.asInstanceOf[Light]
```

note: throws exception on invalid casting

---

# Type Checking

- Scala support run time type checking
- Throws exception on invalid casting
- keywords: __isInstanceOf__, __classOf__
- keywords: __asInstanceOf__ for casting

---

# Class Type Check

Helps to check exact concrete class

```scala
class Appliance {}
class Light extends Appliance {}
val applianceAppliance = new Light;

println(appliance.getClass == classOf[Light])
println(appliance.getClass == classOf[Appliance])
```

prints true for first
prints false for second

---

# Instance Check

```scala
class Appliance {}
class Light extends Appliance {}
val applianceAppliance = new Light;

println(appliance.isInstanceOf[Light])
println(appliance.isInstanceOf[Appliance])
```

prints true for both

---

# Abstract Class

Scala support abstract class, for which instances cannot be created.

```scala
abstract class Appliance (val id: Int,
                    val name: String) {
     override def toString = s"$id, $name"
}
```

Get compilation error if you create object for abstract class

```scala
//doesn't work, fails
val applicance = new Appliance(1, "a1")
```

---


# object

Scala do not support static members. Instead, Scala has singleton object. Scala __object__ shall helps to create singleton object.

```scala
object NumberFactory {
    var id: Int = 0;
    
    def next: Int = {
        id += 1;
        return id
    } 
}
```

NumberFactory is a singleton object

```scala
println(NumberFactory.next)
println(NumberFactory.next)
```

prints 0, 1

---

# object body

__object__ can have body section, which is executed very first use of object. Good for initialize values.

```scala
object NumberFactory {
    var id: Int = 0;
    
    def next: Int = {
        id += 1;
        return id
    } 

    id = 1000;
    println("inside factory", next);
}
```

when we use NumberFactory first time, it prints

    inside factory 1001

---


# Companion Object

A companion object is an object with the same name as a class or trait.

```scala
class Product (var name: String) {
    private var year = 0
    private var id = Product.seq;
    ...
}

object Product {
    var id: Int = 0
    
    def seq(): Int = {
        id += 1;
        id; //return id
    }
    
    def apply(name : String, year: Int): Product = {
        var product : Product = new Product(name)
        product.year = year
        return product
    }
}
```

---

# Companion Object

A companion object is an object with the same name as a class or trait.
 
- Companion object can access Companion class private member
- Companion class can access companion object private members
- Companion object can create companion object working as factory

---

# Companion Object apply()

apply method of object useful to create objects of companion classes

```scala
object Product {
    def apply(name : String, year: Int): Product = {
        var product : Product = new Product(name)
        product.year = year
        return product
    }
}
```
To create object, call like

```scala
Product("Phone 1", 2017)
```

__note__, there is no new statement in above line, it calls
apply method automatically,that creates and returns objects

---

# Companion Object apply()

```scala
class Product (var name: String) {
    private var year = 0
    private var id = Product.seq;
    
    override def toString = s"($name, $id, $year)"
}

object Product {
    var id: Int = 0
    
    def seq(): Int = {
      id += 1;
      id; //return id
    }
    
    def apply(name : String, year: Int): Product = {
      var product : Product = new Product(name)
      product.year = year
      return product
    }
     
}
```

---

# object Access Specifier

A private member cannot accessed outside, only that __object__ can access it.

```scala
object NumberFactory {
    private var id: Int = 0;
    
    private def next: Int = {
        id += 1;
        return id
    } 

    // protected also support, only inherited object can access
}
```

Outside NumberFactory, we cannot use next, since it is private

```scala
//below statement won't work
println(NumberFactory.next)
```

---

# Trait

- is an interface [similar to Java + more]
- Trait can have default implementation
- Useful to make mixins, add additional functionalities
- Multiple traits implementation for class
- Order matters with multiple traits

---

## Example trait for a Switchable Appliance

```scala
trait Switch {
    def on(): Boolean;
    def off(): Boolean;
    def isOn: Boolean
}
```

```scala
trait Controllable {
    def setLevel():
    def getLevel();
}
```

---

## Trait for Energy Consumer
```scala
trait EnergyConsumer {
    def voltage;
    def current
    def energy
}
```

```scala
trait EnergyProducer {
    def voltage;
    def current
    def energy
}
```
