layout: true

.header[Scala Packages]
.footer[Gopalakrishnan Subramani @NodeSense <http://nodesense.ai>]
---

# Intro

![Default-aligned image](scala/assets/scala-functions.png)

---

# import a package

- Import classes, objects from other packages

```scala
import scala.util

var rnd = new util.Random
println(rnd.nextInt())
```

Use _import_ statement to import the libraries. Use _import_ statement to import the libraries. Use _import_ statement to import the libraries. Use _import_ statement to import the libraries

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
- Random can't be accessed outside scope

```scala
def generateRandom : Int = {
    import scala.util.{Random}

    var rnd = new Random
    var n = rnd.nextInt()
    return n;
}
```

---