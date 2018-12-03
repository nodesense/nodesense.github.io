layout: true

.header[Functor]
.footer[Scala]
---

# Functor

- Functor is a Type Class, is not a scala syntax
- A Functor is any data type that defines how map applies to it. 
- In Haskell, it is called as fmap

---

# Functor

- Functor useful to generalize map method
- What map method does? map method lift one value at a time

```scala
def map[A,B](ga: Gen[A])(f: A => B): Gen[B]
def map[A,B](pa: Parser[A])(f: A => B): Parser[B]
def map[A,B](oa: Option[A])(f: A => B): Option[A]
```

How to write a functor

```scala
trait Functor[F[_]] {
def map[A,B](fa: F[A])(f: A => B): F[B]
}
```
---