---
layout: default
title: "File Transfer Techniques: Encryption, HTTP/S, and Living Off the Land"
date: 2026-08-12
categories: [Cybersecurity]
tags: [File Transfer, Encryption, HTTP, HTTPS, Linux, Windows, Living Off the Land]
---

# File Transfer Techniques: Encryption, HTTP/S, and Living Off the Land

Today I continued learning different file transfer techniques, focusing on methods that can help when normal transfer options are restricted.

The main topics I studied were:

* File encryption
* Catching files over HTTP/S
* Living off the Land techniques

The biggest takeaway was that file transfer is not only about moving files, but also about protecting them and adapting to the tools already available on a system.

---

## File Encryption

File encryption can help protect sensitive data before transferring it between systems.

One way to encrypt files is with OpenSSL.

### Encrypt a File

```bash
openssl enc -aes256 -iter 100000 -pbkdf2 -in file.txt -out file.enc
```

This creates an encrypted version of the original file.

### Decrypt a File

```bash
openssl enc -d -aes256 -iter 100000 -pbkdf2 -in file.enc -out file.txt
```

The correct password is required to restore the original file.

### Encrypt with GPG

GPG can also encrypt a file using a password:

```bash
gpg -c file.txt
```

This creates:

```text
file.txt.gpg
```

To decrypt it:

```bash
gpg -d file.txt.gpg > file.txt
```

Encryption is useful when the contents of a transferred file should remain protected.

---

## Catching Files over HTTP

HTTP can be used not only to download files, but also to receive uploaded files.

A Python upload server can be used for this purpose.

### Start an Upload Server

```bash
python3 -m uploadserver 8000
```

This starts a server that listens for uploaded files.

### Upload a File with cURL

```bash
curl -X POST http://<IP>:8000/upload -F 'files=@file.txt'
```

The file is sent to the system running the upload server.

This can be useful when outbound HTTP connections are allowed but other transfer protocols are unavailable.

---

## Catching Files over HTTPS

HTTPS works similarly to HTTP but adds encryption to the connection.

Using HTTPS helps prevent transferred data from being sent in plaintext.

The general idea is:

```text
Client → HTTPS connection → Upload server
```

This provides an additional layer of protection while transferring files over the network.

---

## Living Off the Land

Living off the Land means using tools and utilities that are already installed on the operating system.

Instead of downloading a new transfer tool, existing system utilities can sometimes perform the same task.

This is especially useful when:

* Software installation is restricted
* Only built-in tools are available
* Additional executables cannot be introduced
* Certain transfer utilities are blocked

---

## Windows Living Off the Land

Windows includes several built-in utilities that can be used for file transfers.

### PowerShell

PowerShell can download files directly:

```powershell
Invoke-WebRequest -Uri "http://<IP>/file.txt" -OutFile "file.txt"
```

The shorter alias can also be used:

```powershell
iwr "http://<IP>/file.txt" -OutFile "file.txt"
```

### Certutil

`certutil` can also retrieve files:

```cmd
certutil.exe -urlcache -split -f http://<IP>/file.txt file.txt
```

Although `certutil` is designed for certificate-related tasks, it can also interact with remote URLs.

---

## Linux Living Off the Land

Linux systems also contain many common utilities that can be used for file transfers.

### cURL

```bash
curl http://<IP>/file.txt -o file.txt
```

### Wget

```bash
wget http://<IP>/file.txt
```

### Bash TCP Connection

Bash can sometimes communicate directly through TCP using `/dev/tcp`.

```bash
exec 3<>/dev/tcp/<IP>/8000
```

This demonstrates how built-in shell functionality can sometimes be used when dedicated transfer tools are unavailable.

---

## Quick Workflow Comparison

### File Encryption

```bash
# 1. Encrypt the file
openssl enc -aes256 -iter 100000 -pbkdf2 -in file.txt -out file.enc

# 2. Transfer the encrypted file

# 3. Decrypt it on the destination
openssl enc -d -aes256 -iter 100000 -pbkdf2 -in file.enc -out file.txt
```

### HTTP Upload

```bash
# 1. Start the upload server
python3 -m uploadserver 8000
```

```bash
# 2. Upload the file from the other system
curl -X POST http://<IP>:8000/upload -F 'files=@file.txt'
```

### Living Off the Land on Windows

```powershell
# Download using PowerShell
Invoke-WebRequest -Uri "http://<IP>/file.txt" -OutFile "file.txt"
```

```cmd
REM Download using certutil
certutil.exe -urlcache -split -f http://<IP>/file.txt file.txt
```

### Living Off the Land on Linux

```bash
# Using wget
wget http://<IP>/file.txt

# Using curl
curl http://<IP>/file.txt -o file.txt
```

---

## What I Learned

Today I learned that file transfer techniques can be adapted depending on the environment.

For example:

* Encryption can protect sensitive files before they are transferred.
* HTTP/S can be used to receive files when other protocols are unavailable.
* Living off the Land techniques make use of tools already installed on the system.
* Windows and Linux both provide built-in utilities that can perform file transfers.

The more transfer methods I understand, the easier it becomes to choose an appropriate technique for a specific environment.

---

## Key Takeaway

The most important lesson from today was that successful file transfer depends on understanding both the network and the available system tools.

Being familiar with encryption, HTTP/S transfers, and built-in utilities provides more flexibility when common file transfer methods are restricted.
