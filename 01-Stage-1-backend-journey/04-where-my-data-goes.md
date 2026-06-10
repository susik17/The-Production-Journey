

# Where My Data Goes

I created:

```http
POST /users
```

The API worked.

But there was a problem.

When I restarted the application:

```text
Data disappeared.
```

Why?

Because data was only stored in memory.

Memory is temporary.

When the process stops, memory is cleared.

I needed permanent storage.

## Enter PostgreSQL

This is where databases come in.

```text
Application
      ↓
PostgreSQL
```

Now user data survives application restarts.

Examples:

```text
Users
Orders
Products
Payments
```

can all be stored safely.

## Another Problem

My application works with Java objects.

Example:

```java
User user = new User();
```

But PostgreSQL understands SQL.

Example:

```sql
INSERT INTO users
```

Now I had to constantly convert:

```text
Java Object
      ↓
SQL Query
      ↓
Database
```

and later:

```text
Database Row
      ↓
Java Object
```

Doing this everywhere became repetitive.

## Enter Hibernate

Hibernate acts as a translator.

Instead of writing SQL manually:

```sql
INSERT INTO users
```

I can simply write:

```java
userRepository.save(user);
```

Hibernate generates the SQL behind the scenes.

Flow:

```text
Java Object
      ↓
Hibernate
      ↓
SQL
      ↓
PostgreSQL
```

This made database operations much easier.

At this point:

```text
API ✓
Database ✓
Persistence ✓
```

I thought I was done.

I was wrong.

The real challenges started when the application entered production.