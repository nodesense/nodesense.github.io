layout: true

.header[SBT]
.footer[Gopalakrishnan Subramani @NodeSense <http://nodesense.ai>]
---

# Simple Build Tool

- Simple Build Tool
- aka Scala Build Tool
- or SBT
- A build system similar to Maven
- A Scala DSL
- Easy and Intuitive

---

# SBT

- Interactive Build tool
- Command Line Interface
- Compile, Run Scala Applications

---

# SBT

- Configuration
- Tasks for the projects
- Similar to maven in Java
- Similar convention over configuration approach
- Keeps source files in src/main/scala
- Keeps test files in src/test/scala

---

# build.sbt

```scala
organization := "ai.nodesense.myproject"
scalaVersion := "2.12.3"
version := “1.0-SNAPSHOT"
```

---

# build.sbt

```scala
libraryDependencies ++= Seq(
    "joda-time" % "joda-time" % "2.9.2",
    "org.joda" % "joda-convert" % "1.8"
)


libraryDependencies += "org.scalatest" % “scalatest_2.12” % "3.0.4" % "test"

```

---

```bash
    > sbt
    [info] sbt server started at 127.0.0.1:5609
    
    To compile application

    sbt:myproject> compile

    To run application

    sbt:myproject> run

    Reload the set file if any changes

    sbt:myproject> reload

    Open Scala cli, this helps to import any packages mentioned in build.sbt

    sbt:myproject> console

    scala> :q 
```

---

# SBT

```
    > sbt
    > helps
    > settings
    > tasks  
```

```
    > sbt build
    > sbt compile
    > sbt run
    > sbt run 
    > sbt package
```

---

# Root config

```scala
lazy val root = (project in file(".")).
  settings(
    inThisBuild(List(
      organization := "ai.nodesense",
      scalaVersion := "2.11.12",
      version      := "0.1.0-SNAPSHOT"
    )),
    name := “sparkpro"
    ...
```

---

# Packages

```scala
libraryDependencies ++= {
  val sparkVer = "2.3.0"
  Seq(
    "org.apache.spark" %% "spark-core" % sparkVer ,
    "org.apache.spark" %% "spark-sql" % sparkVer    ,
    "org.apache.spark" %% "spark-streaming" % sparkVer,
    "org.apache.spark" %% "spark-mllib" %  sparkVer
  )
},
```
---

# Provided Scope

Use this when only needs compile time dependencies,
at runtime, these libraries already loaded by process 

```scala

libraryDependencies += "org.apache.hadoop" % "hadoop-hdfs" % "2.7.3"  % "provided" ,
// https://mvnrepository.com/artifact/org.apache.hadoop/hadoop-common
libraryDependencies += "org.apache.hadoop" % "hadoop-common" % "2.7.3" % "provided",
```

---

# Resolve Conflicts

```scala

assemblyMergeStrategy in assembly := {
  case PathList("javax", "servlet", xs @ _*) => MergeStrategy.last
  case PathList("javax", "activation", xs @ _*) => MergeStrategy.last

  case "about.html" => MergeStrategy.rename
  case "META-INF/ECLIPSEF.RSA" => MergeStrategy.last
 
  case "git.properties" => MergeStrategy.last
  case "log4j.properties" => MergeStrategy.last
  case x =>
    val oldStrategy = (assemblyMergeStrategy in assembly).value
    oldStrategy(x)
}
```

---

# SBT Get Started
 
    > sbt new scala/scala-seed.g8

give project name starter
   
    > cd starter
	
change package name in build.sbt
and folder name to starter

change the package name to  "com.starter" for test and source code.

    > sbt run

Now it downloads required dependent modules

and prints "hello"

---

# Packaging

Build a jar file.

Add below to build.sbt.

    mainClass := Some("com.starter.Hello")

Run package command for package creation

    > sbt package

Creates a file jar file target/scala-2.12/starter_2.12-0.1.0-SNAPSHOT.jar

---

# Run the jar file

package file produces the light jar file, doesn't include scala libraries.

    > scala  target/scala-2.12/starter_2.12-0.1.0-SNAPSHOT.jar

this prints

"hello"

This jar file shall not work in java runtime due to dependencies.

---

# Uber Jar/FAT JAR

Produces a "fat jar" (which includes all dependencies, including the Scala libraries).

This method is suitable for Java Deployment too.

---

# sbt-assembly

this deploy the fat jars, includes dependencies

Add below to project/assembly.sbt file

    addSbtPlugin("com.eed3si9n" % "sbt-assembly" % "0.14.6")

run below command

    sbt assembly

and produces target/scala-2.12/starter-assembly-0.1.0-SNAPSHOT.jar

---

# Run the jars

    > java -jar target/scala-2.12/starter-assembly-0.1.0-SNAPSHOT.jar

prints 
"hello"

or 

run using scala

    > scala target/scala-2.12/starter-assembly-0.1.0-SNAPSHOT.jar

    > java -cp myjar.jar com.mypackage.myClass

    > java -cp sparkpro-assembly-0.1.0-SNAPSHOT.jar ai.nodesense.util.FeedData