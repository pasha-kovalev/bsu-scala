## СТРОКИ, КОМПАРАТОРЫ И ФИЛЬТРЫ
#### 1. What is the output of the following code?

```
val s = "Hello, world!"
val t = s"$s.length is ${s.length}"
println(t)
```

- **Hello, world!.length is 13**
- s.length is 13
- Hello, world! length is 13
- length is 13

#### 2. What is the output of the following code?

```
val fruits = List("apple", "banana", "cherry")
val sorted = fruits.sortWith(_ > _)
println(sorted)
```

- List(apple, banana, cherry)
- List(apple, cherry, banana)
- List(banana, cherry, apple)
- **List(cherry, banana, apple)**


#### 3. How can you filter a list of strings based on a regular expression?
- val filtered = list.filter(s => s.matches(regex.toString))
- val filtered = list.filter(regex.findFirstIn(_).isDefined)
- val filtered = for (s <- list if s.matches(regex.toString)) yield s
- **Any of the above**

#### 4. What is the output of the following code?

```
val names = List("Alice", "Bob", "Charlie", "Kanye")
val result = names match {
  case List(a, b, c) => s"$a, $b, and $c"
  case List(a, b, _*) => s"$a, $b, and others"
  case _ => "Unknown"
}
println(result)
```

- Alice, Bob, and Charlie
- **Alice, Bob, and others**
- Unknown
- MatchError


#### 5. What is the output of the following code?
```
val list = List("apple", "banana", "cherry", "aloe")
val regex = "a.*e".r

val filtered = list.foldLeft(List.empty[String]) { (acc, s) =>
  if (s.matches(regex.toString)) s :: acc else acc
}.reverse

println(filtered)
```
- List(aloe, apple, banana, cherry) 
- List(aloe, apple)
- **List(apple, aloe)**
- List(aloe, cherry, banana, apple)

#### 6. When using pattern matching, which character matches on any object?
- `%`
- ->`_`
- `^`
- `-`

## ДИЗАЙН КОДА С ЛЯМБДА ВЫРАЖЕНИЯМИ
#### 1. What is the output of the following code?

```
var sum = 0
val adder = (x: Int) => { sum += x }
sum = 10
adder(5)
println(sum)
```
- 5
- 10
- **15**
- Compilation error

#### 2. Which of the following options correctly represents a pure function ?

- **(x: Int) => x + 1**
- (x: Int) => println(x)
- List(1, 2, 3).map(_ + 1)
- (x: Int) => { println(x); x + 1}


#### 3. Which of the following options correctly represents correct monadic function using the Either monad?

- (x: Int) => Right(x)
- (x: Int) => x + 1
- **(x: Int) => if (x > 0) Right(x) else Left("Negative value")**
- (x: Int) => Left(x)

#### 4. What is the output of the following code?

```
val numbers = List(1, 2, 3)
val sum = numbers.foldLeft(6)(_ + _)
println(sum)
```

- 0
- 6
- **12**
- 24


#### 5. How can currying be implemented with lambdas?

```
def curriedSum(x: Int)(y: Int):Int = ???
```

- `y => x + y`
- `x -> ((y: Int) => x + y)`
- `On -> x + y`
- -> `x + y`


## ВЗАИМОДЕЙСТВИЕ С РЕСУРСАМИ

#### 1. What is the difference between Source.fromFile and Source.fromResource?

- **Source.fromFile reads a file from the file system, while Source.fromResource reads a file from the classpath.**
- Source.fromFile reads a file from the classpath, while Source.fromResource reads a file from the file system.
- Both Source.fromFile and Source.fromResource read files from the file system.
- Both Source.fromFile and Source.fromResource read files from the classpath.

#### 2. What is the purpose of the scala.util.Using class?
- To handle exceptions in Scala programs.
- **To manage resources that need to be closed properly.**
- To provide utility methods for working with collections.

#### 3. What method of the buffered writer makes data to be written to the file immediately?

- writer.write()
- writer.sync()
- writer.commit()
- **writer.flush()**

## ОПТИМИЗАЦИЯ РЕКУРСИИ

#### 1. What is the primary advantage of using tail recursion over regular recursion?

- **Tail recursion eliminates the risk of stack overflow errors.**
- Tail recursion provides better performance than regular recursion.
- Tail recursion simplifies the implementation of recursive algorithms.
- Tail recursion allows for more concise code compared to regular recursion.


####  2. What is the output of the following code?
```
import scala.annotation.tailrec 
 
@tailrec 
def factorial(n: Int): Int =
{ 
    if (n == 1) 
        1
    else 
        n * factorial(n - 1) 
} 

println(factorial(3)) 
```

- 6
- 2
- 24
- **error**


#### 3. What should replace the ??? in the code snippet to complete the tail-recursive implementation of the factorial function?

```
import scala.annotation.tailrec

def factorial(n: Int): Int = {
  @tailrec
  def factorialHelper(n: Int, acc: Int): Int = n match {
    case 1 => acc
    case _ => ???
  }

  factorialHelper(n, 1)
}
```

- factorialHelper(n, (n + 1) * acc)
- n * factorialHelper(n - 1,  acc)
- **factorialHelper(n - 1, n * acc)**
- n * acc


## КОМПОЗИЦИЯ ЛЯМБД

####  1. What is the output of the following code?

```
val square: Int => Int = x => x * x
val negate: Int => Int = x => -x

val combined: Int => Int = square andThen negate
val result = combined(5)

println(result)
```

- 25
- **-25**
- 5
- Compilation error

#### 2. What is the output of the following code?

```
val add: Int => Int = _ + 1
val multiply: Int => Int = _ * 2

val composed: Int => Int = multiply.compose(add)

val res: Int = composed(1)

println(res)
```
- 1
- 2
- 3
- **4**

#### 3. What is the output of the following code?

```
val add: Int => Int = _ + 1
val multiply: Int => Int = _ * 2

val composed: Int => Int = multiply.andThen(add)

val res: Int = composed(1)

println(res)
```
- 1
- 2
- **3**
- 4

#### 4. Which of the following options demonstrates how you can use a lambda expression to design a higher-order function that takes a list and a lambda expression to transform each element of the list?
- `def transformList[A, B](list: List[A], f: B => A): List[B] = list.map(f)`
- -> `def transformList[A, B](list: List[A], f: A => B): List[B] = list.map(f)`
- `def transformList[A, B](list: List[A], f: A => B): List[A] = list.map(f)`
- `def transformList[A, B](list: List[A], f: B => A): List[A] = list.map(f)`

#### 5. Which of the following options demonstrates how you can use lambda expressions to design a higher-order function that performs an operation on two input values?

- `def performOperation[A](a: A, b: A, f: A => A): A = f(a, b)`
- -> `def performOperation[A](a: A, b: A, f: (A, A) => A): A = f(a, b)`
- `def performOperation[A](a: A, b: A, f: A => A): A = f(a) + f(b)`
- `def performOperation[A](a: A, b: A, f: (A, A) => A): A = f(a) + f(b)`
