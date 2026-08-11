---

title: "File Transfer Techniques I Learned"
date: 2026-08-10
categories: [Cybersecurity]
tags: [File Transfer, Linux, Windows, PowerShell, SMB, FTP, Base64]
-------------------------------------------------------------------

# File Transfer Techniques I Learned

Today I studied several ways to transfer files between Linux and Windows systems.

The main methods I practiced were:

* Base64 encoding and decoding
* PowerShell downloads and uploads
* SMB file transfers
* FTP downloads and uploads

The biggest takeaway was that different environments require different transfer methods, so it is useful to know multiple options.

---

## Base64 Encode and Decode

Base64 can be useful when normal file transfer methods are not available and the file needs to be moved through terminal text.

### Encode a File

```bash
base64 file.txt
```

To save the encoded output:

```bash
base64 file.txt -w 0 > encoded.txt
```

The result will look similar to:

```text
SGVsbG8gV29ybGQK
```

### Decode a File

```bash
echo "SGVsbG8gV29ybGQK" | base64 -d > file.txt
```

This recreates the original file from the Base64 data.

---

## PowerShell Download

PowerShell provides several built-in methods for downloading files on Windows.

### Invoke-WebRequest

```powershell
Invoke-WebRequest -Uri "http://<IP>/file.exe" -OutFile "file.exe"
```

The shorter alias can also be used:

```powershell
iwr "http://<IP>/file.exe" -OutFile "file.exe"
```

### WebClient

Another option is using `Net.WebClient`:

```powershell
(New-Object Net.WebClient).DownloadFile(
    "http://<IP>/file.exe",
    "C:\Windows\Temp\file.exe"
)
```

This downloads the remote file and saves it to the specified Windows path.

---

## PowerShell Upload

PowerShell can also upload files to a server that accepts HTTP uploads.

```powershell
Invoke-RestMethod -Uri "http://<IP>:8000/upload" -Method Post -InFile "file.txt"
```

The receiving system must have a server configured to accept the uploaded file.

---

## SMB File Transfer

SMB is commonly used for Windows file sharing.

A Linux system can create an SMB share using Impacket.

### Start the SMB Server

```bash
sudo impacket-smbserver share $(pwd) -smb2support
```

Here:

```text
share
```

is the name of the SMB share, while:

```text
$(pwd)
```

shares the current Linux directory.

### View the Share from Windows

```cmd
dir \\<IP>\share
```

### Download a File from the Share

```cmd
copy \\<IP>\share\file.exe .
```

### Upload a File to the Share

```cmd
copy file.txt \\<IP>\share\
```

SMB is especially useful in Windows environments because network shares are supported natively.

---

## FTP Download and Upload

FTP is another common protocol for transferring files.

### Connect to the FTP Server

```bash
ftp <IP>
```

After connecting, FTP provides its own interactive commands.

### Download a File

```text
get file.txt
```

### Upload a File

```text
put file.txt
```

### Download Multiple Files

```text
mget *
```

### Upload Multiple Files

```text
mput *
```

Standard FTP is easy to use, but it does not encrypt traffic by default.

---

## Quick Workflow Comparison

### Base64

```bash
# 1. Encode the file
base64 file.txt -w 0

# 2. Copy the encoded data

# 3. Decode it on the other system
echo "<BASE64_DATA>" | base64 -d > file.txt
```

### PowerShell Download

```powershell
# 1. Specify the remote file
$url = "http://<IP>/file.exe"

# 2. Download it
Invoke-WebRequest -Uri $url -OutFile "file.exe"

# 3. Confirm the file exists
Get-Item .\file.exe
```

### SMB Transfer

```bash
# 1. Start an SMB share from Linux
sudo impacket-smbserver share $(pwd) -smb2support
```

```cmd
REM 2. View the share from Windows
dir \\<IP>\share

REM 3. Download the file
copy \\<IP>\share\file.exe .
```

### FTP Transfer

```bash
# 1. Connect to the FTP server
ftp <IP>
```

```text
# 2. Download a file
get file.txt

# 3. Upload a file
put file.txt

# 4. Exit FTP
bye
```

---

## What I Learned

Today I learned that file transfer is not just about memorizing one command.

The best method depends on the system and environment.

For example:

* Base64 can work when only terminal text is available.
* PowerShell is useful on Windows systems.
* SMB works well when Windows network sharing is available.
* FTP provides simple download and upload commands.

Knowing several techniques gives me more options when one method is blocked or unavailable.

---

## Key Takeaway

The most important lesson from today was to understand the environment first and then choose the appropriate file transfer technique.

Being comfortable with multiple tools and commands will make file transfers much easier during future cybersecurity labs and exercises.
