# Java 17 Features – Explained with Examples

Java 17 is another Long-Term Support (LTS) release and brings several new language features, enhancements, and finalized preview APIs. Here's a curated list of key features with code examples.

---

## ✅ 1. Sealed Classes
**Purpose**: Restrict which classes can extend or implement a superclass.

```java
public sealed interface Shape permits Circle, Square {}
final class Circle implements Shape {}
final class Square implements Shape {}
```

---

## ✅ 2. Pattern Matching for `instanceof`
**Purpose**: Eliminate casting boilerplate after type checks.

```java
Object obj = "Java";
if (obj instanceof String s) {
    System.out.println(s.toUpperCase());
}
```

---

## ✅ 3. Switch Expressions (Standardized)
**Purpose**: Use switch as an expression, return values, and avoid fall-through.

```java
String day = "MONDAY";
int num = switch (day) {
    case "MONDAY", "TUESDAY" -> 1;
    case "WEDNESDAY" -> 2;
    default -> 0;
};
System.out.println(num);
```

---

## ✅ 4. `record` Classes (Introduced in Java 14, Stable Now)
**Purpose**: Concise syntax for immutable data classes.

```java
public record Person(String name, int age) {}

Person p = new Person("Alice", 30);
System.out.println(p.name() + " is " + p.age());
```

---

## ✅ 5. Text Blocks (Standardized)
**Purpose**: Handle multi-line strings more naturally.

```java
String json = """
    {
        "name": "Alice",
        "age": 30
    }
    """;
System.out.println(json);
```

---

## ✅ 6. Enhanced Pseudo-Random Number Generator API (JEP 356)
**Purpose**: Unified and extensible PRNG interface.

```java
RandomGenerator generator = RandomGeneratorFactory.of("L64X256MixRandom").create();
System.out.println(generator.nextInt());
```

---

## ✅ 7. JEP Highlights
- JEP 409: Sealed Classes
- JEP 406: Pattern Matching for `instanceof`
- JEP 382: New macOS Rendering Pipeline (for Apple Silicon)
- JEP 391: macOS/AArch64 Port

---

## ✅ 8. Deprecations & Removals
- RMI Activation removed
- Applet API deprecated (fully removed in Java 21)

---

## 💡 Summary
Java 17 cements several modern features into the Java language and JVM, making code cleaner, safer, and more expressive. As an LTS release, it’s highly recommended for production use going forward from Java 11.

---
