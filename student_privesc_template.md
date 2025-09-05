# 🧪 Student Pentest Walkthrough Template

## 📥 Getting Started

This template is where you’ll track everything you did during your privilege escalation lab.

It mirrors how real penetration testers write reports, track steps, document evidence, and prove exploitation. Your job is to **fork this repo, clone it to your machine, edit this file, then push your work back to your GitHub account**.

---

## 🔹 How to Fork & Use This Template

### 💻 GitHub Desktop Walkthrough for Students

If you’re more comfortable with a graphical interface than the command line, follow these instructions to complete your student pentest walkthrough using **GitHub Desktop**.

---

## 📦 Step-by-Step Instructions

### 🔹 1. Install GitHub Desktop
- Download from: [https://desktop.github.com](https://desktop.github.com)
- Install and log in with your GitHub account

---

### 🔹 2. Fork the Instructor’s Repo
1. Navigate to the [instructor’s GitHub repo](https://github.com/anombyte93/student_privesc) in your browser
2. Click **Fork** in the top-right corner
3. This creates a personal copy under your GitHub username
4. Now you can just edit online by clicking 'edit' on the template. Alternatively, continue following the steps below to edit on your local computer.

---

### 🔹 3. Clone Your Fork with GitHub Desktop
1. Open GitHub Desktop
2. Click **File > Clone Repository**
3. Select the repo you just forked from the list
4. Choose a local folder to store your files
5. Click **Clone**

---

### 🔹 4. Create and Edit Your Walkthrough
1. Open the folder GitHub Desktop cloned to
2. Locate `Student_Privesc_Template.md`
3. Copy it and rename it:

```bash
walkthrough-YOURNAME.md
```

4. Open the file with a text editor (e.g., VSCode, Notepad++, Sublime Text)
5. Fill out each section as you complete the lab

---

### 🔹 5. Commit and Push Changes
1. Return to GitHub Desktop
2. You’ll see your edited file listed under **Changes**
3. In the summary box, type a message like:

```
"Added my privesc lab walkthrough"
```

4. Click **Commit to main**
5. Click **Push origin** to upload changes to your GitHub fork

---

### 🔹 6. Submit Your Work
- Go to your GitHub profile and find your forked repo
- Confirm your `walkthrough-YOURNAME.md` is visible
- Copy the repo URL and submit it as your lab report

---

## 💡 Why This Is Important
- ✅ GitHub is how professionals document, collaborate, and version-control projects
- ✅ Submitting work this way shows you're job-ready
- ✅ Your walkthrough becomes part of your personal cybersecurity portfolio

---

> 💬 If you're stuck at any step, ask your instructor or teaching assistant for help!

## 💻 Alternatively you can fork using the command line

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

