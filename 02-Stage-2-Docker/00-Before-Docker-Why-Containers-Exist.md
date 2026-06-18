# 00 - Before Docker: Why Containers Exist

## The Question I Wanted to Answer

Before learning Docker, I had a simple question:

> If my application runs on my laptop, why do we need Docker at all?

To answer that, I had to understand what happens before Docker even enters the picture.

---

## Everything Starts With an Operating System

Applications cannot run directly on hardware.

They need an Operating System.

For example:

```text
Laptop
    +
Ubuntu
    =
Usable Computer
```

The operating system manages:

* CPU
* Memory
* Storage
* Processes
* Networking

Without an OS, there is no place for an application to run.

---

## The Old Approach

Imagine a company has three applications:

```text
Student Service
Payment Service
Notification Service
```

All of them are installed on the same server.

```text
Server
 ├── Student Service
 ├── Payment Service
 └── Notification Service
```

At first, everything looks fine.

Then problems start.

* One application consumes all memory
* One application crashes
* Different applications need different software versions

Now every application affects the others.

---

## Virtual Machines

To solve this, virtualization was introduced.

Instead of one server running everything together, we can create multiple virtual servers.(logical seperation)

```text
Physical Server
       |
   Hypervisor
       |
  ----------------
  |      |      |
 VM1    VM2    VM3
```

Each VM behaves like a separate computer.

Example:

```text
VM1 → Backend API
VM2 → Database
VM3 → Monitoring
```

This gives isolation and better control.

---

## Where Does AWS EC2 Fit?

AWS => EC2 => Virtualization Concept  =>  
physical server -> logical seperations -> EC2 instances

When I launch an EC2 instance:

```text
EC2 Instance
```

I am actually creating a Virtual Machine.

Example:

```text
Ubuntu EC2
```

becomes:

```text
AWS Datacenter (more servers)
        |
      VM
        |
     Ubuntu
```

So before Docker, I first created:

```text
Root User (AWS account)
      ↓
IAM User (for security)
      ↓
EC2 Instance (server)
      ↓
SSH Connection(for connect with my own laptop)
```

and got access to my own Linux server.

---

## The Limitation of Virtual Machines

VMs solve many problems.

But every VM contains its own operating system.

```text
VM1
 └── Ubuntu

VM2
 └── Ubuntu

VM3
 └── Ubuntu
```

This means:

* More RAM usage
* More storage usage
* Slower startup

Sometimes we don't need an entire operating system just to run one application. we just need part of OS only.
Eg:VM1 => 10GB => Application needs only 5GB => remaing waste 

---

## Enter Containers

Containers take a different approach.

Instead of creating a full OS every time, containers share the host operating system.

```text
Server
    |
 Host OS
    |
 Containers
```

Example:

```text
Container 1 → Backend API
Container 2 → PostgreSQL
Container 3 → Redis
```

Each application is isolated, but there is no extra operating system inside every container.

Because of this, containers are:

* Lightweight
* Faster to start
* Easier to move between environments

---

## Why Docker Became Popular

Suppose I build a Spring Boot application.

On my laptop:

```text
Java 21
Maven
Dependencies
```

Everything works.

I move the application to another server.

Suddenly:

```text
Java missing
Wrong version
Missing libraries
```

The application fails.

Classic developer problem:

```text
"It works on my machine."
```

---

## Docker's Idea
#### Docker => implements containarization

Docker packages everything an application needs.

```text
Application
    +
Runtime
    +
Dependencies(application & system)
    +
Configuration
```

into a single image.

That image can then run anywhere Docker is installed.

```text
Laptop
      |
Docker Image
      |
EC2 Server
```

Same image.

Same behavior.

---

## The Architecture I Built

During this learning journey, the actual flow looked like this:

```text
My Laptop
      |
      | SSH
      |
      v
AWS EC2 (Virtual Machine)
      |
Docker Engine
      |
Docker Container
      |
Application
```

This is where Docker fits.

Docker is not the server.

Docker is not the cloud.

Docker is a layer that sits on top of a server and provides a consistent environment for applications.

---

## Key Takeaways

```text
OS => Runs the machine

VM => Virtual computer 

EC2 => AWS virtual machine

Container => Lightweight isolated environment

Docker => Tool that creates and manages containers

Image => Blueprint

Container => Running instance
```

---

## Next

Now that the foundation is clear, the next question becomes:

> "How did I actually create a server, connect to it, install Docker, and run my first container?"

That journey continues in:

```text
01-where-does-docker-actually-fit.md
```
