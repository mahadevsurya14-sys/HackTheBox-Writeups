# HTB - TrueSecrets

**Platform:** Hack The Box  
**Challenge:** TrueSecrets  
**Category:** Digital Forensics / Memory Forensics  
**Difficulty:** Easy  
**XP:** 260  
**Status:** Solved

## Overview

TrueSecrets is a digital forensics challenge focused on investigating a Windows memory dump to recover information related to an encrypted development environment and a custom Command and Control (C2) server.

## Tools Used

- Kali Linux
- Volatility 3
- TrueCrypt / tcplay
- Python 3
- OpenSSL
- Linux forensic utilities

## Investigation Walkthrough

### 1. Memory Dump Analysis

- Identified the Windows operating system using Volatility.
- Investigated running processes and command-line arguments.
- Identified TrueCrypt and relevant archive activity.

### 2. File Recovery

- Used `windows.filescan` to locate the development archive.
- Recovered the archive using `windows.dumpfiles`.
- Extracted the encrypted TrueCrypt container.

### 3. TrueCrypt Credential Recovery

- Investigated TrueCrypt process memory.
- Identified references to the encrypted container.
- Used Volatility's `windows.truecrypt.Passphrase` plugin to recover a cached passphrase.

### 4. Encrypted Volume Analysis

- Identified the TrueCrypt volume.
- Used tcplay to inspect and map the encrypted container.
- Accessed the decrypted FAT12 filesystem in read-only mode.

### 5. C2 Source Code Analysis

Recovered `AgentServer.cs` and performed static code analysis.

Identified:
- TCP-based C2 communication.
- Session identification using GUIDs.
- DES-based session log encryption.
- Base64-encoded encrypted log data.

### 6. Session Log Investigation

- Identified the encryption implementation in the C# source code.
- Used Python and OpenSSL for offline log decryption.
- Investigated the recovered session activity.
- Located the challenge's final evidence.

## Key Learnings

- Windows memory forensics using Volatility 3.
- Recovering files from memory dumps.
- Investigating cached credentials.
- TrueCrypt volume analysis.
- Static analysis of C# source code.
- DES-CBC encryption and Base64 decoding.
- Digital forensic investigation and evidence handling.

## Conclusion

This challenge demonstrated how sensitive credentials cached in memory can expose encrypted data and how insecure cryptographic practices can compromise sensitive session logs.

**Status: Successfully Completed**
