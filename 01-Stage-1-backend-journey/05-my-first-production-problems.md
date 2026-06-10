# My First Production Problems

Building an API was easy.

Running it reliably was harder.

As soon as real users started using the application, new problems appeared.

---

## Problem 1: Bad Data

I assumed users would send valid data.

Bad assumption.

Somebody can send:

```json
{
  "name": "",
  "email": "abc"
}
```

Without validation:

```text
Bad Data
    ↓
Database
```

Eventually the system becomes messy.

Validation acts like a security guard.

It checks requests before they enter the application.

---

## Problem 2: Things Fail

In production:

- Databases fail
- Networks fail
- APIs fail

Failures are normal.

Without exception handling:

```text
500 Internal Server Error
```

Users get confusing responses.

Exception handling converts failures into meaningful messages.

Example:

```json
{
  "message": "User not found"
}
```

---

## Problem 3: Half Finished Operations

Suppose creating a user involves:

1. Create User
2. Create Wallet
3. Create Audit Record

What happens if step 2 fails?

```text
User Created ✓
Wallet Failed ✗
Audit Missing ✗
```

Now the system is inconsistent.

Transactions solve this.

Rule:

```text
Everything succeeds

OR

Everything rolls back
```

---

## Problem 4: Debugging

One day a user says:

> The application is not working.

My first question becomes:

> What happened?

Without logs:

```text
Nobody knows.
```

With logs:

```text
Request Started
User Created
Database Timeout
Request Failed
```

Logs become the application's memory.

---

## Problem 5: Different Environments

Soon I had:

```text
Development
Testing
Production
```

Each environment needed different settings.

Example:

```text
application-dev.properties
application-prod.properties
```

Profiles help Spring load the correct configuration.

---

## Problem 6: Monitoring

Now operations teams started asking questions.

```text
Is the application healthy?
How much memory is used?
How many requests are coming?
```

The application needed to expose this information.

This is where Actuator helps.

Examples:

```http
/actuator/health
```

```http
/actuator/metrics
```

---

## Problem 7: Security

Without security:

```http
DELETE /users/1
```

Anyone could call it.

Applications need to answer two questions:

```text
Who are you?
What are you allowed to do?
```

Spring Security helps enforce these rules.

---

## Problem 8: JWT

After login:

```text
User
   ↓
Login
   ↓
JWT Token
```

The client stores the token.

For future requests:

```text
Request
   ↓
JWT Token
   ↓
Backend
```

The backend identifies the user using the token.

---

## Problem 9: Filters

Before a request reaches a controller, some checks should happen.

Examples:

- Is the JWT valid?
- Is the request allowed?
- Should this request be logged?

Flow:

```text
Request
   ↓
Filter
   ↓
Controller
```

Filters allow these checks to happen once for every request.

---

## Problem 10: Performance

As traffic increased, the database started receiving the same queries repeatedly.

Example:

```http
GET /countries
```

thousands of times.

Instead of querying the database every time:

```text
Request
   ↓
Cache
   ↓
Database (only if needed)
```

This reduces database load and improves response time.

---

## Problem 11: Growing Systems

Eventually one application became many services.

```text
User Service
Email Service
Payment Service
Analytics Service
```

Now services needed a way to communicate.

This is where Kafka appears.

Instead of:

```text
User Service
      ↓
Email Service
```

we can do:

```text
User Service
      ↓
Kafka
      ↓
Email Service
```

Services become less dependent on each other.

This improves reliability and scalability.

---

# End of Stage 1

At the beginning of this journey, I only had:

```java
public static void main(String[] args)
```

By the end, I understood:

- How Java runs
- What the JVM does
- Why Tomcat exists
- Why Spring exists
- How APIs work
- Why databases are needed
- What Hibernate does
- Why validation matters
- Why transactions matter
- Why logging matters
- How security works
- Why caching exists
- Why Kafka exists

Now I have a much clearer picture of what actually happens inside a backend application.

This foundation will help me understand Docker, CI/CD, Kubernetes, Cloud, DevOps, and SRE concepts much more naturally.