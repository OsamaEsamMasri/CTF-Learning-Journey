# Forensics 101
<img width="573" height="288" alt="لقطة شاشة 2026-05-09 161541" src="https://github.com/user-attachments/assets/cc48c5cc-71b1-484b-b785-a8034693a7c5" />

## Platform
CTFLearn

## Category
Forensics

## Difficulty
Easy

---

# Challenge Description

The challenge provided a downloadable JPG image and hinted that the flag was hidden somewhere inside the file.

---

# Objective

Analyze the image file and recover the hidden flag.

---

# Initial Analysis

First, I checked the file type using:

```bash
file 95f6edfb66ef42d774a5a34581f19052.jpg
```
<img width="1058" height="86" alt="لقطة شاشة 2026-05-09 162106" src="https://github.com/user-attachments/assets/6e921ed5-34e7-4e71-b3fd-9a64ea849e2f" />

Output:

```text
JPEG image data, JFIF standard 1.01
```

The file appeared to be a normal JPG image.

---

# Metadata Inspection

I used `exiftool` to inspect the image metadata:

```bash
exiftool 95f6edfb66ef42d774a5a34581f19052.jpg
```
<img width="696" height="408" alt="لقطة شاشة 2026-05-09 162115" src="https://github.com/user-attachments/assets/fa293100-4cc4-4c87-a6b1-1f8ecca74112" />
The metadata did not reveal anything suspicious.

---

# Extracting Readable Strings

Next, I used the `strings` command to search for readable text inside the file:

```bash
strings 95f6edfb66ef42d774a5a34581f19052.jpg
```
<img width="730" height="373" alt="image" src="https://github.com/user-attachments/assets/a459a1c5-ed51-4fc8-a50c-0018a2e6be40" />

After reviewing the output, I found the flag directly embedded inside the image:
<img width="436" height="141" alt="image" src="https://github.com/user-attachments/assets/4375c718-fbff-4d12-bd8c-54e51add322f" />


---

# Flag

```text
flag{wow!_data_is_cool}
```

---

# Tools Used

- file
- exiftool
- strings

---

# What I Learned

- How to inspect unknown files in forensic challenges
- Using `file` to identify file types
- Using `exiftool` to inspect metadata
- Using `strings` to extract readable text from binary files
- Some CTF flags may be directly embedded inside files
