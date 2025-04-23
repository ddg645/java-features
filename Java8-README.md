# Java 8 Features – Explained with Examples

Java 8 introduced powerful features that changed the way we write Java code. This README captures the most important additions with real-world working examples.

---

## ✅ 1. Lambda Expressions
**Purpose**: Enable passing behavior as a method argument.

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
names.forEach(name -> System.out.println("Hello, " + name));
```

---

## ✅ 2. Streams API
**Purpose**: Functional-style operations on collections.

```java
List<String> names = Arrays.asList("Tom", "Jerry", "Spike");
List<String> result = names.stream()
    .filter(name -> name.startsWith("S"))
    .map(String::toUpperCase)
    .collect(Collectors.toList());
System.out.println(result); // Output: [SPIKE]
```

---

## ✅ 3. Default Methods in Interfaces
**Purpose**: Add new methods to interfaces without breaking existing implementations.

```java
interface Vehicle {
    void drive();
    default void honk() {
        System.out.println("Honking from Vehicle!");
    }
}

class Car implements Vehicle {
    public void drive() {
        System.out.println("Driving a car.");
    }
}

Car car = new Car();
car.drive();
car.honk();
```

---

## ✅ 4. Functional Interfaces
**Purpose**: Interface with a single abstract method, ideal for lambda use.

```java
@FunctionalInterface
interface GreetingService {
    void greet(String name);
}

GreetingService greet = message -> System.out.println("Hello, " + message);
greet.greet("World");
```

---

## ✅ 5. Optional Class
**Purpose**: Avoid NullPointerExceptions and represent absent values explicitly.

```java
Optional<String> name = Optional.ofNullable("John");

name.ifPresentOrElse(
    val -> System.out.println("Name is: " + val),
    () -> System.out.println("No name provided")
);

String defaultName = name.orElse("Default");
System.out.println("Result: " + defaultName);
```

---

## ✅ 6. New Date and Time API (`java.time`)
**Purpose**: Thread-safe, immutable date/time classes.

```java
LocalDate today = LocalDate.now();
LocalTime now = LocalTime.now();
LocalDateTime timestamp = LocalDateTime.now();

DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm");
String formatted = timestamp.format(formatter);

System.out.println("Today: " + today);
System.out.println("Now: " + now);
System.out.println("Formatted: " + formatted);
```

---

## 💡 Summary
Java 8 made Java more expressive, readable, and concise by enabling functional programming paradigms and improving core APIs. Each of the features above contributes to modern, clean, and maintainable Java code.

---
