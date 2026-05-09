# Taking LS

## Platform
CTFLearn

## Category
Forensics

## Difficulty
Easy

---

## Challenge Description

The challenge provided a ZIP file from a Mega link and hinted that the flag would remain hidden.

---

## Steps

### 1. Downloading the File

First, I downloaded the ZIP file from the provided Mega link.

```text
Mega link: https://mega.nz/file/mCgBjZgB#_FtmAm8s_mpsHr7KWv8GYUzhbThNn0I8cHMBi4fJQp8
```

---

### 2. Extracting the ZIP File

After downloading the file, I extracted it using:

```bash
unzip The\ Flag.zip
```
<img width="493" height="208" alt="image" src="https://github.com/user-attachments/assets/121cfd51-9b30-49fb-9d2f-fac92e43dd84" />

After extraction, I noticed that a folder named `The Flag` was created.

Inside the extracted folder, I noticed a hidden directory named `.ThePassword`.

In Linux systems, files or directories that start with a dot `.` are considered hidden files.

```bash
ls
```

Output:
<img width="428" height="69" alt="image" src="https://github.com/user-attachments/assets/088bc95f-e4b8-4c86-a2d5-7c47a899329b" />

```text
__MACOSX
The Flag
The Flag.zip
```

---

### 3. Opening the PDF File

Inside the extracted folder, there was a PDF file:

```text
The Flag.pdf
```

When I tried to open it, the PDF required a password.

This suggested that the flag was likely stored inside the protected PDF file.
---
<img width="673" height="700" alt="image" src="https://github.com/user-attachments/assets/86b2b00a-8b2e-455d-953a-069951d858d4" />

### 4. Searching for Hidden Files

Because the challenge name is **Taking LS**, I used the Linux `ls` command with the `-la` option to show hidden files:

```bash
cd "The Flag"
ls -la
```

This revealed a hidden directory:

```text
.ThePassword
```
<img width="523" height="146" alt="image" src="https://github.com/user-attachments/assets/254eec70-f3a4-424f-8e0b-969e97921108" />

---

### 5. Reading the Hidden Password File

I entered the hidden directory:

```bash
cd .ThePassword
```

Then I listed its contents:

```bash
ls
```

I found a file named:

```text
ThePassword.txt
```

I displayed its content using:

```bash
cat ThePassword.txt
```

This gave me the password needed to unlock the PDF.
<img width="501" height="176" alt="image" src="https://github.com/user-attachments/assets/9b6cac63-3efa-4352-b9ea-85423d1cb177" />
---

### 6. Unlocking the PDF

After finding the password, I opened the protected PDF file and entered the password:

```text
Im The Flag
```

The PDF successfully opened and revealed the flag inside the document.


<img width="625" height="656" alt="image" src="https://github.com/user-attachments/assets/c6b2a053-24fe-4111-adec-66c63d93a029" />


---

## Flag

```text
ABCTF{T3Rm1n4l_is_C00l}
```

---

## Tools Used

- unzip
- ls
- cd
- cat
- PDF viewer

---

## What I Learned

- How to extract ZIP files in Linux
- How to use `ls -la` to reveal hidden files and directories
- Hidden files in Linux usually start with a dot `.`
- A password-protected file may have its password hidden somewhere nearby
- Basic forensic investigation depends on checking all extracted files carefully
