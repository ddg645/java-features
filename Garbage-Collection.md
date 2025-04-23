# ☕ Java Garbage Collection (GC) Cheat Sheet

A quick reference to understand, choose, and tune garbage collectors across Java versions.

---

## 🔧 Common GC JVM Flags

| Flag | Description |
|------|-------------|
| `-XX:+UseSerialGC` | Use Serial (single-threaded) GC |
| `-XX:+UseParallelGC` | Use Parallel GC (aka Throughput Collector) |
| `-XX:+UseG1GC` | Use Garbage First GC (default in Java 9+) |
| `-XX:+UseZGC` | Use Z Garbage Collector (very low pause) |
| `-XX:+UseShenandoahGC` | Use Shenandoah GC (very low pause) |
| `-XX:+UseEpsilonGC` | Use No-op GC (testing only) |
| `--enable-preview` | Required for preview GCs (like Generational ZGC) |

---

## 📊 When to Use Which GC?

| GC Type | Use Case | Heap Size | Latency |
|---------|----------|-----------|---------|
| Serial | Simple apps, embedded | Small (<1GB) | High |
| Parallel | Batch jobs, background work | Medium–Large | Medium |
| G1 | General-purpose, responsive UI/server apps | Medium–Large | Low |
| ZGC | Real-time systems, microservices, huge heaps | 8MB–16TB | **Very Low** |
| Shenandoah | Low-latency JVM apps (e.g., financial trading) | Medium–Large | **Very Low** |
| Epsilon | Performance testing only (no GC!) | N/A | N/A |

---

## 🚀 GC Command Examples

```bash
# G1GC (Java 8+)
java -XX:+UseG1GC MyApp

# ZGC (Java 11+)
java -XX:+UnlockExperimentalVMOptions -XX:+UseZGC MyApp

# Shenandoah (Java 12+, stable in Java 17+)
java -XX:+UseShenandoahGC MyApp

# Epsilon GC
java -XX:+UnlockExperimentalVMOptions -XX:+UseEpsilonGC MyApp

# Generational ZGC (Java 21 Preview)
java --enable-preview -XX:+UseZGC -XX:+ZGenerational MyApp
```

---

## 📈 Monitor GC Performance

```bash
# Print GC logs
-verbose:gc -XX:+PrintGCDetails -XX:+PrintGCDateStamps

# Use Java Flight Recorder (JFR)
-XX:+UnlockCommercialFeatures -XX:+FlightRecorder

# Enable GC summary stats
-Xlog:gc*:file=gc.log
```

---

## 🧪 Sample Benchmarking Code

```java
public class GCTest {
    public static void main(String[] args) {
        for (int i = 0; i < 1_000_000; i++) {
            String[] array = new String[1000];
            for (int j = 0; j < array.length; j++) {
                array[j] = "value" + j;
            }
        }
        System.out.println("Allocation test done");
    }
}
```

Run with different GC options and compare GC logs or profiling tools.

---

## ⚙️ GC Tuning Parameters for Heap Sizing

| Parameter | Purpose | Example |
|-----------|---------|---------|
| `-Xms<size>` | Set initial heap size | `-Xms512m` |
| `-Xmx<size>` | Set max heap size | `-Xmx4g` |
| `-XX:NewRatio` | Ratio of old/new gen | `-XX:NewRatio=2` → 1/3 young, 2/3 old |
| `-XX:SurvivorRatio` | Ratio of Eden to Survivor spaces | `-XX:SurvivorRatio=6` → 6:1:1 |
| `-XX:MaxTenuringThreshold` | Age at which objects move to old gen | `-XX:MaxTenuringThreshold=10` |

Use these to balance between memory consumption and pause time.

---

## 🧾 Reading GC Logs – Quick Guide

Typical GC log output (G1GC):
```
[GC pause (G1 Evacuation Pause) (young), 0.0123456 secs]
   [Parallel Time: 10.0 ms, GC Workers: 4]
   [Eden: 50M(50M)->0B(60M) Survivors: 10M->10M Heap: 100M(200M)->60M(200M)]
```

### Key Parts:
- **GC Type**: e.g., G1 Evacuation Pause
- **Pause Time**: Time app was paused (e.g., `0.0123 sec`)
- **Eden/Survivor**: How much space was used before → after
- **Heap**: Total usage before → after GC

Look for:
- 💡 **High pause times** → try ZGC/Shenandoah
- 📉 **High promotion rate** → tune `NewRatio`, `MaxTenuringThreshold`
- 💣 **Full GC often** → check for memory leaks, use `-Xlog:gc+heap=debug`

---

## 🎯 GC Tuning Profiles by Application Type

### ✅ API Servers (Low-latency, responsive)
```bash
-Xms512m -Xmx2g \
-XX:+UseG1GC \
-XX:MaxGCPauseMillis=100 \
-XX:+UseStringDeduplication
```
- GC: G1GC for predictable latency
- Use `MaxGCPauseMillis` to control pause goals

### ✅ Data Processing Pipelines (Throughput-oriented)
```bash
-Xms4g -Xmx16g \
-XX:+UseParallelGC \
-XX:+UseCompressedOops \
-XX:+UseLargePages
```
- GC: Parallel GC for batch jobs
- Prioritize throughput over pause time

### ✅ Microservices (Scalable, concurrent)
```bash
-Xms512m -Xmx2g \
-XX:+UseZGC \
-XX:+TieredCompilation \
-XX:+UseNUMA
```
- GC: ZGC for ultra-low pause times
- Use with containers or Kubernetes

### ✅ Messaging/Event-driven Apps (Low-latency spikes)
```bash
-Xms1g -Xmx8g \
-XX:+UseShenandoahGC \
-XX:+AlwaysPreTouch \
-XX:MaxGCPauseMillis=50
```
- GC: Shenandoah for low-pause under bursty workloads
- `AlwaysPreTouch` improves GC predictability on large heaps

---

### ✅ Real-Time Trading Systems
```bash
-Xms1g -Xmx4g \
-XX:+UseShenandoahGC \
-XX:+AlwaysPreTouch \
-XX:+UseNUMA \
-XX:MaxGCPauseMillis=10
```
- Shenandoah GC helps with ultra-low-latency trading apps.
- NUMA-aware tuning enhances CPU/memory locality.

### ✅ Apache Spark Apps (Driver/Executor)
```bash
-Xms8g -Xmx16g \
-XX:+UseG1GC \
-XX:MaxGCPauseMillis=200 \
-XX:+UseStringDeduplication \
-XX:+AlwaysPreTouch \
-XX:+HeapDumpOnOutOfMemoryError
```
- G1GC balances large heap processing with predictable pause behavior.
- Common tuning for data-intensive ETL or ML Spark jobs.

### ✅ Kubernetes JVM Operators
```bash
-XX:+UseG1GC \
-XX:+UseContainerSupport \
-XX:InitialRAMPercentage=40.0 \
-XX:MaxRAMPercentage=75.0 \
-XX:+HeapDumpOnOutOfMemoryError \
-XX:+ExitOnOutOfMemoryError
```
- Works seamlessly in memory-restricted Kubernetes pods.
- Helps avoid OOM kills and enables diagnostic logs.

---

### ✅ Spring Boot Applications
```bash
-Xms512m -Xmx2g \
-XX:+UseG1GC \
-XX:MaxGCPauseMillis=100 \
-XX:+UseContainerSupport \
-XX:+HeapDumpOnOutOfMemoryError
```
- G1GC fits latency-sensitive workloads
- Container-aware heap sizing ensures better k8s behavior

---

### ✅ Kafka Consumers
```bash
-Xms1g -Xmx4g \
-XX:+UseZGC \
-XX:MaxGCPauseMillis=50 \
-XX:+UseNUMA \
-XX:+DisableExplicitGC
```
- ZGC ensures responsiveness and consistent event consumption

---

### ✅ Java-based ETL Pipelines
```bash
-Xms4g -Xmx8g \
-XX:+UseParallelGC \
-XX:+UseCompressedOops \
-XX:+UseLargePages \
-XX:+HeapDumpOnOutOfMemoryError
```
- ParallelGC offers throughput efficiency for heavy transformations

---

### ✅ Large-Scale Batch Analytics
```bash
-Xms16g -Xmx32g \
-XX:+UseParallelGC \
-XX:+UseStringDeduplication \
-XX:+HeapDumpOnOutOfMemoryError \
-XX:+AlwaysPreTouch
```
- ParallelGC maximizes throughput; PreTouch reduces runtime hiccups

---

### ✅ Serverless JVM Apps
```bash
-XX:+UseSerialGC \
-Xms128m -Xmx512m \
-XX:+TieredStopAtLevel=1 \
-XX:+ExitOnOutOfMemoryError
```
- Fast startup and minimal overhead for cold-start sensitivity

---

### ✅ GraalVM Native Image
```bash
--no-server \
--native-image-info \
-H:+ReportUnsupportedElementsAtRuntime \
-H:+TraceClassInitialization \
-H:Name=myApp
```
- GraalVM flags for optimizing ahead-of-time compiled binaries
- Monitor image build and runtime behavior precisely

---
