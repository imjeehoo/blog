---
title: 'How to Mount SFTP as a Drive on Mac'
description: 'Learn how to mount SFTP servers as local drives on macOS using SSHFS, making remote file access as easy as browsing local folders.'
publishedAt: 'June 08 2025'
---

Transferring files to and from remote servers is a common task—but constantly switching between clunky SFTP clients like FileZilla or CyberDuck can interrupt your workflow. What if you could access those remote files just like any other folder on your Mac?

With **SSHFS (SSH Filesystem)**, you can mount a remote SFTP server as a local drive, making file access fast, seamless, and native to macOS.

## What is SFTP Drive Mounting?

SFTP (Secure File Transfer Protocol) drive mounting allows you to connect a remote directory and treat it like a local disk in Finder. Instead of launching separate apps, you can browse, open, and edit remote files directly from your Mac’s file system.

---

## Requirements

Before we get started, you’ll need:

- macOS with admin privileges
- [Homebrew](https://brew.sh/) installed
- Access to an SFTP server (username, host, and credentials)

## Installation Steps

### 1. Install Required Tools

Open Terminal and install the necessary components:

```bash
# Install macFUSE (formerly known as OSXFuse)
brew install --cask macfuse

# Install SSHFS
brew install sshfs
```

You might be prompted to approve macFUSE in **System Preferences > Security & Privacy**.

### 2. Create a Local Mount Directory

Create a local directory where the remote files will be accessible:

```bash
mkdir ~/sftp-mount
```

### 3. Mount the SFTP Server

Use the following command structure to mount your SFTP server:

```bash
sshfs username@hostname:/remote/path ~/sftp-mount -o volname=MyServer,volicon=icon.png
```

**Example:**
```bash
sshfs john@example.com:/home/john ~/sftp-mount -o volname=RemoteDrive,volicon=/Users/john/Pictures/remote-drive-icon.png
```

### 4. Optional - Enhance Mount Stability

For a more robust connection, you can add additional options:

```bash
sshfs username@hostname:/remote/path ~/sftp-mount \
  -o volname=MyServer,reconnect,ServerAliveInterval=15
```

**Useful options:**
- `volname=MyServer`: Sets a custom name for the mounted drive
- `reconnect`: Automatically reconnects if the connection drops
- `ServerAliveInterval=15`: Sends keep-alive packets every 15 seconds

---

## Unmounting the Drive

You can unmount your drive in three ways:

### Method 1: Terminal
```bash
umount ~/sftp-mount
```

### Method 2: Finder
- Right-click the mounted drive and select **Eject**
- Or use the eject button in Finder's sidebar

### Method 3: Force unmount (if needed)
```bash
sudo diskutil umount force ~/sftp-mount
```

---

## Conclusion

Mounting SFTP as a drive on Mac transforms how you work with remote files. Instead of juggling multiple applications and manual file transfers, you get seamless integration with your local file system. This "clean" approach to remote file access can significantly improve your workflow when working with remote servers.

Whether you're a developer accessing deployment servers, a content creator managing remote assets, or anyone who regularly works with files on remote systems, SSHFS provides an elegant solution that feels native to macOS.

---

**Resources:**

- https://sftptogo.com/blog/kr/how-to-mount-sftp-as-a-drive-on-mac-kr/
- https://sbeeniny.github.io/posts/study/general/filetrasfer/