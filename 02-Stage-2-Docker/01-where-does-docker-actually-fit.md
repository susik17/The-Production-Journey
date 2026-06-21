# 01 - The Problem Docker Is Trying To Solve

In the previous chapter, I understood:

```text
Physical Server
      ↓
Virtual Machine (EC2)
      ↓
Ubuntu OS
```

At this point, I had my own Linux server running in AWS.

I could connect using SSH:

```bash
ssh -i key.pem ubuntu@<public-ip>
```

and run commands on the server.

Everything looked good.

But I still didn't understand why Docker existed.

---

## The Real Problem

Imagine I write a simple Python application.

```python
print("Hello Susi")
```

On my laptop:

```bash
python app.py
```

Output:

```text
Hello Susi
```

Works perfectly.

---

## Moving To Another Server

Now I copy the same application to another server.

```text
Laptop
   |
 app.py
   |
   v
Server
```

Then I run:

```bash
python app.py
```

Suddenly:

```text
python: command not found
```

The application fails.

---

## Why Did It Fail?

Because my laptop and the server are different environments.

Example:

### My Laptop

```text
Ubuntu
Python 3.12
Required Libraries
```

### Server

```text
Ubuntu
Python Missing
```

Same code.

Different environment.

Different result.

---

## The Classic Developer Problem

This situation is so common that it has a famous name.

```text
"It works on my machine."
```

The code works.

The environment is the problem.

---

## First Solution: Install Everything Manually

One solution is:

```text
Server A
  Install Python

Server B
  Install Python

Server C
  Install Python
```

This works.

But after a few months:

```text
Server A -> Python 3.10

Server B -> Python 3.12

Server C -> Python Missing
```

Again problems.

Managing environments becomes difficult.

---

## Docker's Idea

Instead of saying:

> Install Python first, then run my application

Docker says:

> Package everything together.

```text
Python
   +
Application
   +
Dependencies
   =
One Package
```

Docker calls this package:

```text
Image
```

---

# What Is An Image?

Think of an image as a snapshot.

Example:

```text
Ubuntu
Python 3.12
app.py
```

packed together.

```text
+------------------+
| Ubuntu           |
| Python 3.12      |
| app.py           |
+------------------+
```

This complete package is called an image.

---

## Why Is This Useful?

Now I don't care whether the server has Python installed.

Because Python already exists inside the image.

I only need Docker.

```text
Server
    |
 Docker
    |
 Image
```

Same image.

Same behavior.

Everywhere.

---

# Where Are Images Stored?

Now another question appears.

> If images are so important, where do they come from?

Think about source code.

```text
Code
   |
GitHub
```

GitHub stores code.

Similarly:

```text
Images
   |
Docker Hub
```

Docker Hub stores images.

---

## Docker Hub

Docker Hub contains ready-made images such as:

```text
ubuntu
python
nginx
redis
postgres
```

These images are maintained and shared by the community and companies.

---

## My First Docker Command

I ran:

```bash
docker run hello-world
```

At first it looked like a simple command.

But Docker actually performed multiple steps.

---

## What Happened Behind The Scenes?

Docker checked:

```text
Do I already have the hello-world image?
```

If yes:

```text
Create Container
      ↓
Run Container
```

If no:

```text
Docker Hub
      ↓
Download Image
      ↓
Create Container
      ↓
Run Container
```

This is why the command worked even though I never downloaded anything manually.

---

# Image vs Container

This confused me a lot initially.

I thought:

```text
Image = Container
```

But they are different.

---

## Image

An image is just a template.

Nothing is running.

Example:

```text
Ubuntu Image
```

---

## Container

A container is a running instance created from an image. (like class & objects in oops)

Example:

```text
Ubuntu Image
      |
      +---- Container 1
      |
      +---- Container 2
      |
      +---- Container 3
```

One image can create many containers.

---


# My Mental Model

After experimenting, this became my understanding:

```text
Docker Hub
      |
     Image
      |
      v
  Container
      |
      v
 Application Running
```

---

# What I Learned

```text
Docker
    =
    Tool that manages containers

Docker Hub
    =
    Stores images

Image
    =
    Reusable package

Container
    =
    Running instance of an image
```

Most importantly:

```text
Docker was not created to run applications.

Docker was created to make environments consistent.
```

That is the actual problem Docker solves.

---

# Next

Now I understand:

- Why Docker exists
- What problem it solves
- What Docker Hub is
- What an image is
- What a container is

The next question becomes:

> If Docker Hub already has images like Python and Ubuntu, how can I create my own image?

That's where Dockerfiles enter the picture.