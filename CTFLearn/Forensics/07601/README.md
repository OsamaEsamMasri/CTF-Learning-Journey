# 07601
<img width="556" height="287" alt="لقطة شاشة 2026-05-09 175359" src="https://github.com/user-attachments/assets/47721efc-1c6d-4bd3-8703-91c1f3ad7895" />

## Platform
CTFLearn

## Category
Forensics

## Difficulty
Medium

---

# Challenge Description

The challenge provided an image file and hinted that the flag was hidden somewhere inside it.


---

# Objective

Analyze the image and discover the hidden flag.

---

# Step 1 - Opening the Image

First, I opened the image file to inspect it visually.

```bash
eog AGT.png
```

The image itself did not directly reveal the flag.

<img width="301" height="168" alt="image" src="https://github.com/user-attachments/assets/e7060400-9070-4bde-8831-88e9f8770c06" />

---

# Step 2 - Identifying the Real File Type

Next, I checked the actual file type using the `file` command:

```bash
file AGT.png
```

Output:

```text
JPEG image data, JFIF standard 1.01
```

<img width="1038" height="85" alt="image" src="https://github.com/user-attachments/assets/168028de-267e-4b49-a79d-8a66cc9c30f5" />

Although the file extension was `.png`, the file was actually a JPEG image.


---

# Step 3 - Inspecting Metadata

I used `exiftool` to inspect the image metadata:

```bash
exiftool AGT.png
```

The metadata contained normal image information and did not immediately reveal the flag.

<img width="1035" height="480" alt="image" src="https://github.com/user-attachments/assets/da9dfcc9-077d-4d86-afc6-234b49d3dfd0" />


---

# Step 4 - Searching for Readable Strings

I searched the image for readable text using the `strings` command:

```bash
strings AGT.png
```

During the analysis, I discovered several suspicious filenames and directories such as:

```text
Secret Stuff...
Don't Open This...
I Warned You.jpeg
```

This suggested that hidden files or archives were embedded inside the image.

<img width="706" height="325" alt="image" src="https://github.com/user-attachments/assets/f8b21d3f-6dbe-4ed7-a6ef-963eb4fb2470" />

---

# Step 5 - Analyzing the Image with Binwalk

To investigate further, I used `binwalk`:

```bash
binwalk AGT.png
```

The output revealed multiple embedded ZIP archives hidden inside the image file.

```text
Zip archive data
Secret Stuff...
Don't Open This...
I Warned You.jpeg
```

<img width="1112" height="791" alt="image" src="https://github.com/user-attachments/assets/265bd983-8c9a-4af8-9574-c6fb632cfa1e" />


---

# Step 6 - Extracting Hidden Files

I extracted the embedded content using:

```bash
binwalk -e AGT.png
```

This created a new directory named:

```text
_AGT.png.extracted
```

Inside the extracted directory, I found hidden folders and files.

---

# Step 7 - Navigating Through Hidden Directories

I explored the extracted folders step by step:

```bash
cd _AGT.png.extracted
cd "Secret Stuff..."
cd "Don't Open This..."
```

Inside the final folder, I found an image file named:

```text
I Warned You.jpeg
```

<img width="715" height="178" alt="image" src="https://github.com/user-attachments/assets/cd749d95-4a2a-46db-8926-2dfbf37e9f4f" />


---

# Step 8 - Extracting the Flag

Finally, I searched the extracted image for readable content:

```bash
strings "I Warned You.jpeg"
```

While reviewing the output, I found the hidden flag:

```text
ABCTF{Du$t1nS_D0jo}
```
<img width="279" height="111" alt="image" src="https://github.com/user-attachments/assets/500af1bf-1b41-4207-ade2-278407663342" />

---

# Flag

```text
ABCTF{Du$t1nS_D0jo}
```

---

# Tools Used

- eog
- file
- exiftool
- strings
- binwalk

---

# What I Learned

- How to identify misleading file extensions
- How to inspect image metadata
- Using `strings` to detect suspicious hidden content
- Using `binwalk` to detect and extract embedded archives
- How to navigate extracted forensic artifacts
- Recursive forensic investigation techniques

---

# Skills Practiced

- File analysis
- Metadata inspection
- Hidden archive extraction
- Linux file navigation
- Digital forensics workflow
