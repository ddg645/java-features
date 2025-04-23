# Java 21 Features – Explained with Examples

Java 21 is a **Long-Term Support (LTS)** release that finalizes many preview features and introduces powerful concurrency, syntax, and developer productivity tools.

---

## ✅ 1. Virtual Threads (Project Loom – Finalized)
**Purpose**: Lightweight threads for massive concurrency.

```java
Runnable task = () -> System.out.println("Running in thread: " + Thread.currentThread());
Thread.startVirtualThread(task);
```

---

## ✅ 2. Pattern Matching for `switch` (Finalized)
**Purpose**: Use type patterns and guards in `switch`.

```java
static String format(Object obj) {
    return switch (obj) {
        case Integer i -> "int: " + i;
        case String s when s.length() > 5 -> "long string: " + s;
        case String s -> "short string: " + s;
        default -> "unknown";
    };
}
```

---

## ✅ 3. Record Patterns (Finalized)
**Purpose**: Decompose records within pattern matching.

```java
record Point(int x, int y) {}

Object obj = new Point(3, 4);
if (obj instanceof Point(int x, int y)) {
    System.out.println("x = " + x + ", y = " + y);
}
```

---

## ✅ 4. Sequenced Collections
**Purpose**: Ordered List/Set/Map traversal.

```java
SequencedSet<String> set = (SequencedSet<String>) Set.of("a", "b", "c");
System.out.println(set.getFirst()); // prints "a"
```

---

## ✅ 5. String Templates (Preview)
**Purpose**: Inline string interpolation.

```java
String name = "World";
String message = STR."Hello, \{name}!";
System.out.println(message);
```

> Note: Requires `--enable-preview` flag during compilation and runtime.

---

## ✅ 6. Unnamed Classes and Instance Main Methods (Preview)
**Purpose**: Simplify introductory programs.

```java
void main() {
    System.out.println("Hello from Java 21!");
}
```

> Note: Also requires `--enable-preview`.

---

## ✅ 7. Scoped Values (Preview)
**Purpose**: Safe and efficient sharing of immutable data within and across threads.

```java
ScopedValue<String> USER = ScopedValue.newInstance();
ScopedValue.where(USER, "admin").run(() -> {
    System.out.println("User: " + USER.get());
});
```

---

## ✅ 8. Deprecations & Removals
- Final removal of the Applet API.
- Removal of older GC options.

---

## 💡 Summary
Java 21 solidifies modern Java with productivity and performance features like **virtual threads**, **pattern matching**, and **string templates**. It's ideal for concurrent and clean application development.

---
