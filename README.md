# 🔥 Hashcat - Powerful Offline Cracking Tool (Kali Linux)

**Introduction** 
Hashcat is a high-performance offline password cracking tool that can use GPUs (or CPU) to perform dictionary, mask, and rule-based attacks on password hashes.⚡️
(This repo is only for education purpose)
---

## ⚖️ Legal disclaimer — READ FIRST
This material is **only for educational use** on your **own local machine, VM, Docker container, or authorized labs** (TryHackMe/HTB). Never run password cracking tools against public systems or services you do not own or have explicit permission to test. Misuse may be illegal and unethical. 🛡️

---

## 🛠️ Step-by-step commands

### 1) Update & install Hashcat
```bash
sudo apt update
sudo apt install -y hashcat
```
*Update package lists and install Hashcat.* 🔄🧩

---

### 2) Check devices (GPU/CPU detection)
```bash
hashcat -I
```
*See detected devices and drivers — if no GPU shows, install drivers or run CPU-only.* 🔍

---

### 3) Prepare demo wordlist & hash (small & fast)
```bash
head -n 1000 /usr/share/wordlists/rockyou.txt > ~/rockyou-1000.txt
echo "password123" >> ~/rockyou-1000.txt
echo -n "password123" | md5sum | awk '{print $1}' > ~/hashcat-hashes.txt
cat ~/hashcat-hashes.txt
```
*Create a 1000-line subset, ensure demo password present, create raw-MD5 hash and show it.* ⚡🔐

---

### 4) Basic Hashcat dictionary attack (MD5)
```bash
hashcat -m 0 -a 0 ~/hashcat-hashes.txt ~/rockyou-1000.txt
```
*`-m 0` = MD5, `-a 0` = dictionary attack. Cracked results are saved to the potfile.* ⚔️

---

### 5) Show cracked results
```bash
hashcat --show -m 0 ~/hashcat-hashes.txt
```
*Display recovered passwords (hash:password) from the potfile.* ✅

---

### 6) Mask attack example (targeted brute force)
```bash
hashcat -m 0 -a 3 ~/hashcat-hashes.txt '?l?l?l?l?d?d'
```
*`-a 3` = mask attack; `?l` lower-case, `?d` digits. Efficient for known patterns.* 🎯

---

### 7) Wordlist + rules (mutations)
```bash
hashcat -m 0 -a 0 ~/hashcat-hashes.txt ~/rockyou-1000.txt -r /usr/share/hashcat/rules/best64.rule
```
*Apply `best64.rule` to mutate wordlist entries (case changes, suffixes, etc.).* 🔁

---

### 8) Benchmark (device performance)
```bash
hashcat -b
```
*Run a quick benchmark to show device performance* 📈

---

Made with ❤️ by **The Techzeen** — Happy Hacking! 🎉


