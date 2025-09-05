# 🧪 Student Pentest Walkthrough Template

## 📥 Getting Started

This template is where you’ll track everything you did during your privilege escalation lab.

It mirrors how real penetration testers write reports, track steps, document evidence, and prove exploitation. Your job is to **fork this repo, clone it to your machine, edit this file, then push your work back to your GitHub account**.

---

### 🔹 How to Fork & Use This Template

1. **Go to your instructor’s GitHub repository** (e.g., `https://github.com/instructor/linux-privesc-lab`)

2. In the top-right, click **Fork**. This creates your own copy of the project under your GitHub username.

3. On your newly forked repo page:

   Click the green **Code** button → **Copy the HTTPS link**

4. Open a terminal on your Kali machine and run:

```bash
git clone https://github.com/YOUR_USERNAME/linux-privesc-lab.git
cd linux-privesc-lab
```

5. Copy the template file:

```bash
cp Student_Privesc_Template.md walkthrough-YOURNAME.md
```

6. Edit it using any editor (VSCode, Nano, etc.):

```bash
nano walkthrough-YOURNAME.md
```

7. When done, save your file and commit your changes:

```bash
git add walkthrough-YOURNAME.md
git commit -m "My walkthrough for privilege escalation lab"
git push origin main
```

---

### 💡 Why Does This Matter in the Real World?

✅ Penetration testers must document every step they take — what worked, what didn’t, and proof of success

✅ Git-based workflows are how security consultants share notes, write internal red team reports, and track evidence

✅ Recruiters and mentors love seeing proof of practice — this becomes part of your portfolio

---

## 👤 Student Info

- Name:
- Date:
- Kali IP:
- Metasploitable IP:

---

## 🧭 Initial Access

### 🔹 Foothold Method

- What vulnerability did you use to gain access?
- What was the payload?
- Where did you upload it?
- What URL did you visit to trigger the reverse shell?

### 🔹 Listener Details

- What listener did you set up (command)?
- What session did you receive back?
- Paste a sample output (e.g. `meterpreter >`)

---

## 🔍 Enumeration with linPEAS

### 🔹 Kernel Version

```
uname -a output:
```

### 🔹 Notable Findings from linPEAS:

- SUID Binaries:
- Writable Cron Jobs or Scripts:
- Credentials in Files:
- Writable PATH folders:
- Anything linPEAS marked as high-risk:

**Use this to decide on your next step.**

---

## 🚩 Exploitation Path

### 🔹 Chosen Privilege Escalation Vector

- What method did you choose to escalate?
- Why was it possible to exploit?
- What did linPEAS say that helped you decide?

### 🔹 Step-by-Step Exploit Commands

```
[Insert exact commands and what each one does]
```

### 🔹 Post-Exploitation Confirmation

```
whoami
id
```

- What did you see? Prove root access with output.

---

## 💾 Optional: Bonus or Mystery Task Attempt

### 🔹 Task Attempted:

- DirtyCow / GTFOBins / Cron / PATH Hijack / Other

### 🔹 Method Used:

- Describe what you found and how you exploited it:

```
Commands and what they did:
```

### 🔹 Did it work?

- What happened?
- Did it give you root or unexpected results?

---

## 🧠 Reflection

- What did you learn about Linux privilege escalation?
- What would you do differently in a real-world pentest?
- What part confused you or surprised you most?

---

## ✅ Final Submission Instructions

Once your walkthrough is completed:

1. Make sure you’ve pushed the final version of `walkthrough-YOURNAME.md` to your GitHub repo

2. **Submit the link** to your GitHub repo OR create a Pull Request to the instructor repo if requested

3. Ask yourself:

   - Did I clearly explain my exploit chain?
   - Is my proof of root access shown?
   - Could another student or pentester follow my steps?

> This file is your **report**, your **evidence**, and your **portfolio piece**. Treat it like a job submission.

