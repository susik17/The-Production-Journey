# How My App Started Listening

My Java application was running.

But there was a problem.

If somebody opens a browser and sends:

```http
GET /users
```

nothing happens.

Why?

Because my application is not listening on the network.

=> I had code.

=> I had a JVM.

=> I had a running process.

But I didn't have a listener.

Note: Running an application and receiving requests are two different things.

## Enter Tomcat

Something has to sit on a network port and wait for incoming requests => That's the job of a web server.

In the Java world, one common choice is Tomcat.

Tomcat starts listening on a port.

Usually:

```text
8080
```

Now the flow becomes:

```text
Browser
    ↓
 Tomcat
```

When a request arrives:

```http
GET /users
```

Tomcat receives it first.

Without Tomcat, my Java program would still run.

But nobody could access it.

## One More Question

Suppose Tomcat receives a request.

Now what?

How does it know where to send it?

Imagine my project starts growing.

```text
UserController
UserService
UserRepository
EmailService
AuthService
```

Managing all of this manually would quickly become painful.

This is where Spring enters.
