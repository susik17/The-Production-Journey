# From Java File to JVM

Everything started with a simple Java program.

```java
public class Main {

    public static void main(String[] args) {
        System.out.println("Hello World");
    }

}
```

I compiled it.

```bash
javac Main.java
```

Then I ran it.

```bash
java Main
```
=> Java code cant runs directly.
=> The operating system cannot understand Java code. So , Java first converts the source code into bytecode.

```text
Main.java
    ↓
 javac
    ↓
Main.class
```

Now another question appeared.

Who executes this `.class` file?

The answer is the JVM.
JVM => Java virtual machine 

When I run:

```bash
java Main
```

the operating system creates a new process.

Inside that process, the JVM starts.

```text
Operating System
        ↓
   Java Process
        ↓
       JVM
        ↓
    My Program
```

This was an important realization.

The OS does not know anything about:

* Spring Boot
* Controllers
* Services
* Repositories
* Databases

The OS only sees:

* A process
* Memory usage
* CPU usage
* Threads

That's it.

At this point my application is running successfully.

But I discovered a problem.

Nobody can talk to it.
Its just application runs on my machine.

If a user opens a browser and sends:

```http
GET /users
```

Who receives it?

That question leads to the next chapter.
