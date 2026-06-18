# AWS IAM → EC2 → SSH Cheat Sheet

A quick reference for creating an IAM user, launching an EC2 instance, and connecting to it using SSH.

---

# 1. Create IAM User

Login using the AWS Root Account.

Go to:

```text
IAM
→ Users
→ Create User
```

User name:

```text
susi-devops
```

Enable:

```text
Provide user access to AWS Management Console
```

Set password.

Attach permissions:

```text
AdministratorAccess
```

Create the user.

---

# 2. Login as IAM User

Go to:

```text
IAM
→ Dashboard
```

Copy:

```text
AWS Sign-In URL
```

Example:

```text
https://xxxxx.signin.aws.amazon.com/console
```

Login using:

```text
Username: susi-devops
Password: ********
```

From now on, use the IAM user instead of the root account.

---

# 3. Launch EC2 Instance

Go to:

```text
EC2
→ Launch Instance
```

Settings:

```text
Name: docker-lab
AMI: Ubuntu Server
Instance Type: t2.micro
```

Create a new key pair:

```text
docker-lab-key.pem
```

Download and save it safely.

Network settings:

```text
Allow SSH Traffic
```

Launch Instance.

---

# 4. Get Public IP

Go to:

```text
EC2
→ Instances
→ Select Instance
```

Copy:

```text
Public IPv4 Address
```

Example:

```text
13.xx.xx.xx
```

---

# 5. Connect Using SSH

Open terminal.

Move to the folder containing:

```text
docker-lab-key.pem
```

Set correct permissions:

```bash
chmod 400 docker-lab-key.pem
```

Connect:

```bash
ssh -i docker-lab-key.pem ubuntu@PUBLIC_IP
```

Example:

```bash
ssh -i docker-lab-key.pem ubuntu@13.xx.xx.xx
```

---

# 6. Verify Connection

Check current user:

```bash
whoami
```

Expected:

```text
ubuntu
```

Check OS:

```bash
cat /etc/os-release
```

Check hostname:

```bash
hostname
```

---

# Common SSH Problems

## Permission denied (publickey)

Check:

* Correct `.pem` file
* Correct username (`ubuntu`)
* Correct public IP

---

## Connection timed out

Check Security Group:

```text
Inbound Rules
→ SSH
→ Port 22
→ Allowed
```

---

## Permission 0644 too open

Run:

```bash
chmod 400 docker-lab-key.pem
```

Then reconnect.

---

# Quick Flow

```text
Root Account
    ↓
Create IAM User
    ↓
Login as IAM User
    ↓
Create EC2
    ↓
Download Key Pair
    ↓
Get Public IP
    ↓
SSH into EC2
```

That's it.
