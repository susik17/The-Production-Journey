# Phase 0 – Understanding the Build Process

## Why?

Before learning Docker, I wanted to understand **what Docker actually packages**.

A production deployment doesn't start with Docker—it starts with source code. Before an application can be deployed, it must be prepared into a format that can run in production.

---

## Build Flow

```text
Source Code
      │
      ▼
Dependency Management
(Download Required Libraries)
      │
      ▼
Build
(Compile → Test → Package)
      │
      ▼
Artifact
(Deployable Output)
      │
      ▼
Docker Image
      │
      ▼
Container
      │
      ▼
Production
```

---

## Concepts Learned

### Source Code

The code written by the developer.

Examples:

- `Main.java`
- `HelloController.java`
- `UserService.java`

---

### Dependency Management

Applications often use libraries written by other developers.

Example:

```java
@RestController
@GetMapping
```

These annotations are part of Spring Boot, not Java itself.

Dependency management is responsible for:

- Finding required libraries
- Downloading them
- Making them available to the project

Examples:

| Language | Dependency Manager |
|----------|--------------------|
| Java | Gradle / Maven |
| Python | pip |
| Node.js | npm |
| Go | go mod |

---

### Build

The build process prepares the application for execution.

Typical build steps:

- Compile source code
- Run tests
- Package the application

---

### Artifact

An **artifact** is the final output produced by the build process that is ready for deployment.

Examples:

| Language | Artifact |
|----------|----------|
| Java | `.jar` |
| Go | Binary |
| React | `dist/` |
| Python | Source + Dependencies |

---

### Manual Build

Without build tools, the build process can be performed manually.

```bash
javac Main.java
jar cfm app.jar manifest.txt Main.class
java -jar app.jar
```

---

### Build Tools

Build tools automate the entire build process.

Responsibilities:

- Manage dependencies
- Compile source code
- Run tests
- Package the application
- Generate the final artifact

Popular Java build tools:

- Gradle
- Maven

Example:

```bash
./gradlew build
```

Output:

```text
build/libs/app.jar
```

---

## Practical Work Completed

- Created a Java project from scratch
- Compiled Java source manually using `javac`
- Executed bytecode using the JVM
- Created a JAR manually using the `jar` command
- Explored the contents of a JAR (`META-INF`, `MANIFEST.MF`, `.class`)
- Understood the role of the Manifest file
- Compared manual packaging with Gradle automation

---

## Key Takeaways

- Source code is **not** deployed directly.
- External libraries are managed through dependency management.
- The build process converts source code into a deployable format.
- The final deployable output is called an **artifact**.
- Build tools automate repetitive build tasks.
- Docker **does not build** applications—it packages the already-built artifact into a portable runtime environment.
