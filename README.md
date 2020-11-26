# itchallenges

2nd page:
```java
// Its syntax looks like that
(param1, param2, ...) -> expression
(param1, param2, ...) -> { statement1; statement2; ...}

(int a) -> a + 5; // Calculates the sum
a -> a + 5; // or without indicating a type
```

3rd page:
```java
(a, b) -> a * b; // Multiplication of 2 parameters

/*
If the lambda has more than 1 expression,
we can use { } and "return"
*/
(a, b) -> {
	int sum = a + b;
	int avg = sum / 2;
	return avg;
}

/*
A lambda expression can't stand alone in Java as
it needs to be associated to a functional interface.
*/
interface MyInterface {
    int squareOf(int a);
}
	
MyInterface i = a -> a ^ 2;
i.squareOf(3); // Result is 9
```

4th page:
```java
/*
Functional interfaces provide target types for lambda expressions
and method references. Each functional interface has a single abstract method
to which the lambda expression's parameters and return types
are matched or adapted. Example:
*/

interface Comparator<T> {
  int compare(T t1, T t2); // Functional method
}

Comparator<Student> c = 
    (Student a, Student b) -> // Parameters
      	a.getId().compareTo(b.getId()); // Implementation


/* Other examples */
Predicate<T> -> boolean test(T t);
Supplier<T> -> T get();
Consumer<T> -> void accept(T t);
Function<T, V> -> V apply(T t);
BiPredicate<T, U> -> boolean test(T t, U u);
BiConsumer<T, U> -> void accept(T t, U u);
BiFunction<T, U, V> -> V apply(T t, U u);
BinaryOperator<T> -> T test(T t1, T t2);
```

5th page:
```java
Method Reference    | Lambda Form
----------------------------------------------------------
String::toUpperCase | (String s) -> s.toUpperCase()
String::compareTo   | (String a, String b)->a.compareTo(b)
System.out::println | a -> System.out.println(a)
Double::new         | d -> new Double(d)
String[]::new       | (int a) -> new String[a]
```

7th page:
```java
students // Source
	.stream()
  	.map(student -> student.getAddress())
  	.filter(address -> address.isValid())
  	.map(Address::getStreet)
  	.map(String::toUpperCase)
  	.distinct()
  	.limit(5)
  	// All intermediate operations
  	.collect(Collectors.toList()); // Terminal operation
```

8th page:
```java
Input     | Method            | Output
----------------------------------------------------------
1 2 3 4 5 | map(function)      | a b c d e
            // 1 -> a
            
1 2 3 4 5 | flatMap(function)  | a b c d e f g h i j
            // 1 -> [a, b]
            
1 2 3 4 5 | filter(predicate)  | 1   3 4
            // a != 2 && a != 5

1 2 3 4 5 | peek(consumer)     | 1 2 3 4 5
            // side effect

1 2 3 4 5 | limit(int)         | 1 2 3
            // 3

1 2 3 4 5 | skip(int)          |     3 4 5
            // 2
 
1 1 2 1 2 | distinct()         | 1 2
   
4 2 1 5 3 | sorted(comparator) | 1 2 3 4 5
```

9th page:
```java
Input     | Method                 | Output
----------------------------------------------------------
1 2 3 4 5 | findAny(predicate)     | 2 (not guaranteed)
            // a % 2 == 0
1 2 3 4 5 | findFirst(predicate)   | 2 (guaranteed)
            // a % 2 == 0
1 2 3 4 5 | allMatch(predicate)    | true
            // a != 6
1 2 3 4 5 | noneMatch(predicate)   | false
            // a % 2 == 0
1 2 3 4 5 | anyMatch(predicate)    | true
            // a % 2 == 0
1 2 3 4 5 | count()                | 5
  
1 2 3 4 5 | min(comparator)        | Optional(1)
  
1 2 3 4 5 | max(comparator)        | Optional(5)

1 2 3 4 5 | collect(collector)     | List(...)
            // Collectors.toList()
1 2 3 4 5 | forEach(consumer)      | void
            // side effect
1 2 3 4 5 | reduce(binaryOperator) | Optional(15)
            // Integer::sum
```

10th page:
```java
// Optional<String> contains a string or nothing
Optional<String> result = someStream
   .filter(x -> x.length() > 5)
   .findFirst();

// Either length or "" if nothing
int length = result.orElse("").length();

// If there is a value, execute the lambda 
result.ifPresent(x -> results.add(x));
```
