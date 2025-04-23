# Java 11 Features – Explained with Examples

Java 11 (LTS) brought several enhancements over Java 8. Here's a breakdown of key new features with practical code examples.

---

## ✅ 1. `var` in Lambda Parameters
**Purpose**: Use `var` to add annotations or improve readability in lambdas.

```java
List<String> list = List.of("A", "B", "C");
list.forEach((var item) -> System.out.println(item));
```

---

## ✅ 2. HTTP Client API (Standard)
**Purpose**: Replace HttpURLConnection with modern HTTP client supporting sync/async calls.

```java
HttpClient client = HttpClient.newHttpClient();
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://api.github.com"))
    .build();
HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
System.out.println(response.body());
```

---

## ✅ 3. New String Methods
**Purpose**: Improve string manipulation with built-in helpers.

```java
String blank = "   ";
System.out.println(blank.isBlank());       // true
System.out.println("Java\n11".lines().count()); // 2
System.out.println("Hello ".repeat(3));     // Hello Hello Hello 
```

---

## ✅ 4. File Read/Write Enhancements
**Purpose**: Read file content as string or lines easily.

```java
String content = Files.readString(Path.of("sample.txt"));
System.out.println(content);
```

---

## ✅ 5. `Optional.isEmpty()`
**Purpose**: Complement `isPresent()` with clearer semantics.

```java
Optional<String> value = Optional.empty();
System.out.println(value.isEmpty()); // true
```

---

## ✅ 6. Collection Factory Methods (`List.of`, `Set.of`, `Map.of`)
**Purpose**: Create immutable collections quickly.

```java
List<String> fruits = List.of("Apple", "Banana");
Set<String> colors = Set.of("Red", "Green");
Map<String, Integer> ageMap = Map.of("Alice", 30, "Bob", 25);
```

---

## ✅ 7. Launch Single-File Source Code
**Purpose**: Run Java programs without compiling explicitly.

```bash
java HelloWorld.java
```
(If the file contains a `public static void main` method.)

---

## ✅ 8. Deprecated and Removed APIs
- Removal of Java EE modules (`javax.xml.bind`, etc.)
- Removal of CORBA support

---

## 💡 Summary
Java 11 modernizes the Java language with better readability, lightweight syntax, and full HTTP/REST capabilities. It's a great upgrade path from Java 8, especially for enterprises looking for long-term support.

---
