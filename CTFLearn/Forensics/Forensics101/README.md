# Forensics 101

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

The metadata did not reveal anything suspicious.

---

# Extracting Readable Strings

Next, I used the `strings` command to search for readable text inside the file:

```bash
strings 95f6edfb66ef42d774a5a34581f19052.jpg
```

After reviewing the output, I found the flag directly embedded inside the image:

```text
flag{wow!_data_is_cool}
```

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
