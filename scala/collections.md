layout: true

.header[Scala Collections]
.footer[Gopalakrishnan Subramani @NodeSense <http://nodesense.ai>]
---

# Collections

- Mutable Collection
- Immutable Collection

---

# Mutable Collection

- Add Item to the existing list
- Remove Item
- Update item
- Changes are inline

---

# Immutable List

- Immutable List
- List are seq

```scala
var list: List[Int]= List(10,20,30,40,50)

// returns values from 0th index
 > list(0)

// throws out of bound exception
> list(10)
```

---

# Immutable List

```scala
// add item, returns new List
 list = 60 :: list
// remove item(s)
 > val newList = list.filter(_ > 2)

// Take first 5 items

 > list.take(5)
```

---

# List Formation

To form list,
```scala
  1 :: 2 :: Nil // a list
```

to concat two lists,

```scala
  list1 ::: list2  // concatenation of two lists

  list match {
    case head :: tail => "non-empty"
    case Nil          => "empty"
  }
```

---

# List Efficiency

Always use :::. There are two reasons: efficiency and type safety.

x ::: y ::: z is faster than x ++ y ++ z, because ::: is right associative. x ::: y ::: z is parsed as x ::: (y ::: z), which is algorithmically faster than (x ::: y) ::: z (the latter requires O(|x|) more steps).

---

# Crash free lifting

```scala
> var option: Option[Int] = list.lift(20)
 // returns Option[Int] doesn't crash
 // to be used with
     option.isDefined
     option.get
```

---

# Mutable List ListBuffer

- Mutable List

```scala
import scala.collection.mutable.ListBuffer
val listBuffer = ListBuffer(10, 20, 30, 40, 50)

listBuffer -= 10

listBuffer += 60

listBuffer -= (20, 30)

// Remove By Index
listBuffer.remove(2)

// Use ++ for add/remove collections

listBuffer ++= Seq(10, 20, 30)
listBuffer ++= List(10, 20, 30)

// remove first matches

listBuffer --= Seq(10, 20, 30)
```

---

# Immutable Map

- Map is an interface
- HashMap is a implementation

```scala
val states  = Map("AP" -> "Andra Pradesh", 
                  "KA" -> "Karnataka", 
                  "TN" -> "Tamilnadu")

// to get value

states("AP") //returns Andra Pradesh
states("AK") //throws exception NotSuchElement

// Fail safe get
states.get("AP") //returns Option[String]
// Fail safe get
states.get("AK") //returns Option[None]

// contains
states.contains("AP")
```
---

# Map Iteration
```scala
for ((key,value) <- states) 
    printf("key: %s, value: %s\n", key, value)

// or Just Iterate using for Each (provides Tuple)
states.foreach ( state => state._1 + state._2)

states.keys // returns all keys as set
state.values // returns values as collection
```

---

# Mutable Map
```scala
var states = scala.collection
             .mutable.Map("AP" -> "Andra Pradesh", 
                            "KA" -> "Karnataka", 
                            "TN" -> "Tamilnadu")

// add 
states += ("MH" -> "Maharastra")
states += ("ST1" -> "State 1", "ST2" -> "State 2")

// remove 
states -= "ST1"
states -= ("ST1", "ST2")

// update 
states("ST1") = "State 2"
```

---

# Tuples

- Special Types
- Created with paranthesis (10, 20)
- Or arrow (10 -> 20)

```scala
val numbers = (10, 20, 30)
// Note, 1 based index, not zero based
// accessible via numbers._1, numbers._2, & _3 
```