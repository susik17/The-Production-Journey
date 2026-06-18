# 01 - Where Does Docker Actually Fit?

After understanding Operating Systems, Virtual Machines, and Containers, I wanted to answer one practical question:

> Where does Docker actually fit in a real deployment?

Most Docker tutorials start with:

```bash
docker run nginx
```

The problem is that nobody wakes up and starts with Docker.

Before Docker, there must be a machine.

So instead of learning Docker commands immediately, I decided to create the entire path myself.

---

## Starting With Nothing

Initially, I only had:

```text
My Laptop
```

No server.

No Docker.

No application running in the cloud.

If I build a Spring Boot application on my laptop:

```bash
java -jar app.jar
```

it works.

But my laptop is not production.

Applications need a server where they can run continuously.

So the first task was not Docker.

The first task was getting a server.

---

## Creating a Server in AWS

AWS allows us to create Virtual Machines using EC2.

When I launched my first Ubuntu EC2 instance, I was essentially asking AWS:

> "Give me a Linux machine."

After a few seconds AWS provided:

```text
Ubuntu Server
Public IP Address
```

Now the architecture became:

```text
My Laptop
      |
      |
      v
AWS Ubuntu Server
```

At this point I finally had a machine where applications could run.

But there was still one problem.

I had a server.

I couldn't control it.

---

## Connecting to the Server

AWS gave me a key pair during instance creation.

Using that key, I connected through SSH.

```bash
ssh -i docker-lab-key.pem ubuntu@<public-ip>
```

This was probably the most important moment in the entire setup.

Before SSH:

```text
Commands execute on:

My Laptop
```

After SSH:

```text
Commands execute on:

AWS Server
```

Now every command I typed was running inside a machine located somewhere in an AWS data center.

For the first time, I was working on a cloud server instead of my local system.

---

## Finally Installing Docker

Only now did Docker enter the story.

I installed Docker on the Ubuntu server.

```bash
sudo apt update
sudo apt install docker.io -y
```

After installation the architecture changed again.

```text
My Laptop
      |
     SSH
      |
      v
Ubuntu Server
      |
Docker Engine
```

This immediately answered a confusion I had when starting Docker.

Docker is not the server.

Docker is software running on the server.

Just like Git can be installed on Linux.

Just like Java can be installed on Linux.

Docker can also be installed on Linux.

---

## Testing Docker

The first command I executed was:

```bash
docker run hello-world
```

The command worked.

A message appeared.

Container exited successfully.

Simple.

But something interesting happened behind the scenes.

Docker checked:

```text
Do I already have the hello-world image?
```

Since I didn't have it, Docker downloaded it from Docker Hub.

Then Docker:

```text
Image
    ↓
Container
    ↓
Execution
```

and displayed the output.

This was my first container.

---

## Understanding Images

While experimenting, I discovered that images and containers are not the same thing.

An image is a template.

A container is a running instance created from that template.

For example:

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

This idea becomes important later when running applications at scale.

---

## Running Ubuntu Inside Docker

To understand containers better, I started an Ubuntu container.

```bash
docker run -it ubuntu bash
```

Now the architecture looked like this:

```text
My Laptop
      |
     SSH
      |
      v
AWS Ubuntu Server
      |
Docker Engine
      |
Ubuntu Container
```

This was interesting because I was now entering another isolated environment inside the server.

The server itself was already a Virtual Machine.

Inside that Virtual Machine, Docker was creating containers.

For the first time, the VM and Container concepts became clear.

---

## Running My Own Application

Running Ubuntu and hello-world containers was useful, but I wanted to run something I created.

I wrote a simple Python program:

```python
print("Hello Susi")
```

Then I created a Dockerfile.

```dockerfile
FROM python:3.12

COPY app.py .

CMD ["python","app.py"]
```

The most important line was:

```dockerfile
FROM python:3.12
```

Instead of installing Python manually, I started from a ready-made image that already contained Python.

Docker then combined:

```text
Python Image
      +
My Code
      +
Startup Command
```

and produced a new image.

```bash
docker build -t susi-app .
```

---

## The Full Picture

After building and running my own image, the architecture finally made sense.

```text
My Laptop
      |
     SSH
      |
      v
AWS EC2 Virtual Machine
      |
Docker Engine
      |
Docker Container
      |
Application
```

Docker was never the starting point.

The actual journey was:

```text
AWS Account
      ↓
IAM User
      ↓
EC2 Virtual Machine
      ↓
SSH Access
      ↓
Docker Installation
      ↓
Docker Image
      ↓
Docker Container
      ↓
Application
```

Once this flow became clear, Docker stopped feeling like a separate technology.

It became just another layer between the server and the application.

---

## What's Next?

So far, the application only prints a message and exits.

Real applications are different.

They need:

* Ports
* Databases
* Persistent Storage
* Multiple Containers
* Communication between services

The next step is understanding how Docker runs real applications and how multiple containers work together.
