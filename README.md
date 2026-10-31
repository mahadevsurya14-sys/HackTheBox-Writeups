# Hack The Box – Suspicious Threat

**Status:** Completed  
**Date:** 31 October 2026  
**XP:** 260

## Skills Learned
- Linux Rootkit Forensics
- LD_PRELOAD Analysis
- Shared Library Hooking
- Directory Hiding Detection
- getdents64 System Call

- ## HTB Achievement

[View Suspicious Threat Achievement](https://labs.hackthebox.com/achievement/challenge/4061907/746)

## Investigation Summary
Investigated a suspicious Linux shared library loaded through `/etc/ld.so.preload`.

Identified function hooks and discovered a hidden directory using direct `getdents64` syscall analysis.

**Key Learning:** Understanding Linux system calls helps uncover hidden filesystem entries.
