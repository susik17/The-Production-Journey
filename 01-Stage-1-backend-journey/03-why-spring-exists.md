# Why Spring Exists

At this point, I had:

- A Java application
- A JVM
- Tomcat listening on a port

Now I wanted to build a real backend.

So I started creating classes.

```text
UserController
UserService
UserRepository
```

Looks simple.

But soon the application started growing.

```text
UserController
UserService
UserRepository
EmailService
AuthService
PaymentService
NotificationService
```

Now another problem appeared.

How do I create and connect all these objects?

Initially, I could do it manually.

```java
UserRepository repository = new UserRepository();

UserService service =
    new UserService(repository);

UserController controller =
    new UserController(service);
```

For three classes, this is fine.

For hundreds of classes, it becomes painful.

I would have to:

- Create objects
- Store objects
- Connect objects

everywhere.

This is the problem Spring solves.

## What Spring Actually Does

At a high level, Spring mainly does three things:

1. Creates objects
2. Stores objects
3. Connects objects

Instead of manually creating objects:

```java
UserService service =
    new UserService();
```

I can write:

```java
@Service
public class UserService {

}
```

When the application starts, Spring creates the object for me.

## Application Context

Now another question appeared.

Where does Spring keep all these objects?

The answer is:

```text
Application Context
```

Think of it as Spring's warehouse.

```text
Application Context

UserController
UserService
UserRepository
EmailService
```

When one object needs another object:

```java
@Service
public class UserService {

    private final UserRepository repository;

    public UserService(UserRepository repository) {
        this.repository = repository;
    }
}
```

Spring automatically provides it.

This is called:

```text
Dependency Injection
```

## Then Spring Boot Arrived

Using Spring directly required a lot of setup.

Developers had to configure:

- Tomcat
- Dependencies
- Configuration files
- Database connections

Spring Boot reduced most of this work.

Instead of spending hours configuring things, I could start building features quickly.

At this point:

```text
Tomcat ✓
Spring ✓
Spring Boot ✓
```

Now I was finally ready to build my first API.

# Building My First API

Now I wanted users to interact with my application.

So I created my first endpoint.

```http
GET /users
```

When a request arrives, Tomcat receives it first.

```text
Browser
    ↓
Tomcat
```

Tomcat then forwards the request to Spring.

Spring looks for the correct controller.

```java
@RestController
public class UserController {

}
```

Now the flow becomes:

```text
Browser
    ↓
Tomcat
    ↓
Spring
    ↓
Controller
```

## MVC

As applications grow, putting everything inside one class becomes messy.

So responsibilities are separated.

### Controller

Receives requests.

Example:

```http
GET /users
POST /users
```

### Service

Contains business logic.

Examples:

- Validate user data
- Check business rules
- Perform calculations

### Repository

Talks to the database.

Examples:

- Insert data
- Read data
- Delete data

Simple architecture:

```text
Controller
    ↓
Service
    ↓
Repository
```

## Example Flow

Suppose a user creates an account.

Request:

```http
POST /users
```

Controller receives it.

```text
Controller
```

Controller asks Service to process it.

```text
Controller
    ↓
Service
```

Service performs business logic.

Then asks Repository to save it.

```text
Controller
    ↓
Service
    ↓
Repository
```

Everything looked good.

But then I noticed a problem.

Where is the data actually stored?