# 🔐 Cracking Password-Protected PDFs with Johnny (John the Ripper GUI)

This module is part of my **Cybersecurity Internship** at **NetworkWalks**.
It documents, step by step, how to recover the password of protected PDF files using:

- **John the Ripper (Jumbo)** — password/hash cracking engine
- **Johnny** — graphical user interface (GUI) for John the Ripper
- **Online HashCrack** — online tool used to extract the hash from an encrypted PDF

> ⚠️ **Legal / Ethical Notice**
> This walkthrough is for educational purposes only and for testing files you own or are explicitly authorized to test (CTF, training lab, authorized audit). Never use these techniques on files or systems without permission.

---

## 📋 Prerequisites

- Windows 10/11
- Internet connection
- One or more password-protected PDF files (e.g. `My Locked PDF1.pdf`, `My Locked PDF2.pdf`, `My Locked PDF3.pdf`)

---

## Step 1 — Download Johnny and John the Ripper

Go to the official Openwall wiki page: [https://openwall.info/wiki/johnny](https://openwall.info/wiki/johnny)

Download both archives:
- `johnny_2.2_win.zip` (the graphical interface)
- `john-1.9.0-jumbo-1-win64.zip` (the John the Ripper engine, Jumbo version recommended)

![Downloading Johnny and John the Ripper](../images/1.png)

---

## Step 2 — Install Johnny

Launch the `johnny` installer and follow the **Setup Wizard**.

![Johnny Setup Wizard](../images/2.png)

---

## Step 3 — Set the path to John the Ripper

On first launch, Johnny asks for the path to the John the Ripper executable.
Click **Browse** to select it.

![Setting the John the Ripper path](../images/3.png)

Navigate to the `run` folder of John the Ripper Jumbo and select the `john` (or `john.exe`) file.

![Selecting john.exe](../images/4.png)

Once the path is set, Johnny automatically detects the installed version (here *John the Ripper 1.9.0-jumbo-1 OMP [cygwin 64-bit x86_64 AVX2 AC]*).

![John the Ripper detected](../images/5.png)

---

## Step 4 — Prepare the protected PDF files

On the desktop, there are several locked PDFs: `My Locked PDF1`, `My Locked PDF2`, `My Locked PDF3`.

![Locked PDF files on the desktop](../images/6.png)

Trying to open one (here with Microsoft Edge) prompts for a password.

![Password prompt when opening the PDF](../images/7.png)

---

## Step 5 — Extract the hash from the PDF

We use the online tool **Online HashCrack** ([onlinehashcrack.com](https://www.onlinehashcrack.com)) to extract the hash from the PDF, compatible with `pdf2john` and `pdf2hashcat`.

Go to **Tools → PDF hash extractor**.

![Tools menu - PDF hash extractor](../images/8.png)

Select the locked PDF file to analyze.

![Uploading the PDF file](../images/9.png)

The extracted hash appears in the output field.

![Extracted PDF hash](../images/10.png)

---

## Step 6 — Save the hash to a text file

Copy the extracted hash and paste it into a text editor (Notepad).

![Pasting the hash into Notepad](../images/11.png)

Save the file with a clear name, e.g. `hash1.txt`.

![Saving the hash1.txt file](../images/12.png)

> Repeat steps 5 and 6 for each PDF (`hash2.txt`, `hash3.txt`, etc.).

---

## Step 7 — Load the hash into Johnny

In Johnny, click **Open password file** and select the previously created `hash1.txt` file.

![Opening the hash file in Johnny](../images/13.png)

---

## Step 8 — Run the attack

Click **Start new attack**. Johnny/John the Ripper will attempt to recover the password matching the hash (dictionary/incremental attack depending on configuration).

Once the password is found, it is displayed directly in the **Password** column (here: `good-luck`), with the progress bar at 100% and status *1 cracked*.

![Password cracked - good-luck](../images/14.png)

---

## Step 9 — Verify the password on the PDF

Go back to the locked PDF and enter the recovered password (`good-luck`).

![Entering the recovered password](../images/15.png)

The PDF opens successfully 🎉

![PDF successfully unlocked](../images/16.png)

---

## Step 10 — Crack multiple hashes at once

It is possible to load several hash files at the same time (e.g. `hash2` and `hash3`) by selecting them together in the open dialog.

![Opening multiple hash files](../images/17.png)

Run the attack again with **Start new attack**.

![Starting a new attack on multiple hashes](../images/18.png)

Both passwords are recovered: `password1` and `1qaz2wsx` (100% — 2/2 cracked).

![Two passwords cracked](../images/19.png)

---

## Step 11 — Copy a recovered password

Right-click on a recovered password to copy it directly, or to include/exclude it from a future attack.

![Context menu - copy password](../images/20.png)

---

## Step 12 — Verify the remaining cracked PDFs

Open `My Locked PDF3.pdf` and enter the second recovered password (`1qaz2wsx`).

![Entering the recovered password for PDF3](../images/21.png)

The PDF opens successfully, revealing the captured flag:

```
nw{networkwalks_flag_260821_1}
```

![PDF3 successfully unlocked with flag](../images/22.png)

Likewise, `My Locked PDF2.pdf` opens successfully with its own password, revealing another flag:

```
nw{networkwalks_persistence_jtr_270521}
```

![PDF2 successfully unlocked with flag](../images/23.png)

---

## 🧠 Workflow Summary

```
Locked PDF
     │
     ▼
Hash extraction (Online HashCrack / pdf2john)
     │
     ▼
.txt file containing the hash
     │
     ▼
Johnny (GUI) + John the Ripper
     │
     ▼
Plaintext password
     │
     ▼
Unlocked PDF
```

---

## 📚 Resources

- Johnny GUI: https://openwall.info/wiki/johnny
- John the Ripper: https://www.openwall.com/john/
- Online HashCrack: https://www.onlinehashcrack.com

---

*Module completed as part of my Cybersecurity Internship at NetworkWalks.*
