# swe-fundamentals

## JDK, JRE & JVM — A Layer-by-Layer Breakdown

## 🔧 Concrete Walkthrough

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

### Step 1 — You need the JDK

You run `javac HelloWorld.java`. The `javac` compiler (a **JDK tool**) translates your human-readable `.java` source into platform-independent bytecode → `HelloWorld.class`. Without the JDK, you literally cannot perform this step.

### Step 2 — Now you only need the JRE

You run `java HelloWorld`. At this point, `javac` is irrelevant. What happens is:

- The **JVM** (inside the JRE) loads `HelloWorld.class`, verifies the bytecode is safe, and begins interpreting/JIT-compiling it into native machine code.
- `System.out.println` calls into `java.io.PrintStream`, which is part of the **Class Libraries** (also inside the JRE). Without these libraries bundled in the JRE, even this trivial print statement would fail.

### Step 3 — The end-user experience

When you ship your app to a user's laptop, they don't need `javac` or `jdb`. They just need the **JRE** installed so the JVM + libraries can run your `.class` files.

---

## 🧩 The Superset Relationship

```
JDK
├── JRE
│   ├── JVM  (bytecode → native execution)
│   └── Class Libraries
│       ├── java.lang        — Core classes (String, Math, Object, Thread, System)
│       ├── java.util        — Data structures & utilities (ArrayList, HashMap, Optional, Date)
│       ├── java.io          — File & stream I/O (File, InputStream, BufferedReader)
│       ├── java.nio         — Non-blocking / channel-based I/O (ByteBuffer, Path, Files)
│       ├── java.net         — Networking (Socket, URL, HttpURLConnection)
│       ├── java.sql         — Database access via JDBC (Connection, Statement, ResultSet)
│       ├── java.math        — Arbitrary-precision arithmetic (BigInteger, BigDecimal)
│       ├── java.time        — Modern date/time API (LocalDate, Instant, Duration, ZonedDateTime)
│       ├── java.text        — Formatting & parsing (DateFormat, NumberFormat, MessageFormat)
│       ├── java.security    — Cryptography & access control (MessageDigest, KeyStore, Signature)
│       ├── java.concurrent  — Multithreading utilities (ExecutorService, CountDownLatch, ConcurrentHashMap)
│       ├── java.stream      — Functional-style bulk operations on collections (Stream, Collectors)
│       ├── java.reflect     — Runtime class inspection & manipulation (Method, Field, Constructor)
│       ├── java.logging     — Built-in logging framework (Logger, Handler, Formatter)
│       └── javax.crypto     — Encryption & decryption (Cipher, SecretKey, KeyGenerator)
│
└── Development Tools
    ├── javac       — Compiler: .java source → .class bytecode
    ├── java        — Launcher: starts the JVM and runs bytecode
    ├── jdb         — Debugger: step through code, set breakpoints, inspect variables
    ├── javadoc     — Doc generator: extracts Javadoc comments into HTML API docs
    ├── jar         — Archiver: packages .class files + resources into a .jar bundle
    ├── javap       — Disassembler: inspects bytecode inside .class files
    ├── jdeps       — Dependency analyzer: shows which modules/packages a JAR depends on
    ├── jlink       — Custom runtime builder: creates a minimal JRE with only needed modules
    ├── jpackage    — Installer creator: builds native installers (.exe, .deb, .dmg) from JARs
    ├── jconsole    — Monitoring tool: live view of memory, threads, CPU via JMX
    ├── jvisualvm   — Profiler: CPU/memory profiling, heap dumps, thread analysis
    ├── jmap        — Memory mapper: dumps heap memory for offline analysis
    ├── jstack      — Thread dumper: captures stack traces of all running threads (deadlock diagnosis)
    ├── jstat       — GC statistics: real-time garbage collector performance metrics
    ├── jshell      — REPL: interactive Java shell for quick experiments (since Java 9)
    ├── keytool     — Certificate manager: manages keystores, SSL certs, and trust chains
    └── serialver   — Serial version helper: computes serialVersionUID for Serializable classes
```

> **Key takeaway:** Each outer layer is a strict superset. You can't have the JDK without having the JRE, and you can't have the JRE without having the JVM.