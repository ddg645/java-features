# ☕ Java LTS Feature Guides (Java 8 → 21)

This repository contains detailed guides for major Long-Term Support (LTS) versions of Java: **Java 8, 11, 17, and 21**. Each guide includes feature highlights, working code examples, and migration tips.

---

## 🔍 Contents

| Java Version | Highlights | Link |
|--------------|------------|------|
| **Java 8**   | Lambda, Streams, Optional, Default Methods, Date/Time API | [Java 8 Features](./Java8-README.md) |
| **Java 11**  | HTTP Client, `var` in lambdas, String/Files enhancements | [Java 11 Features](./Java11-README.md) |
| **Java 17**  | Sealed classes, Pattern Matching, Records, Text Blocks | [Java 17 Features](./Java17-README.md) |
| **Java 21**  | Virtual Threads, Scoped Values, String Templates | [Java 21 Features](./Java21-README.md) |

---

## 📌 Purpose

This repo is intended to help:
- 📘 Interview prep with runnable feature demos
- 🔄 Migrate codebases between LTS versions
- 🚀 Refresh knowledge for Java professionals

---

## 🛠 How to Run

Each README includes code snippets. To try them out:
1. Use a JDK 8, 11, 17, or 21 as appropriate
2. Copy the code into your IDE or `*.java` file
3. Compile and run using `javac` and `java` commands

Some features (like preview ones in Java 21) require:
```bash
--enable-preview --source 21
