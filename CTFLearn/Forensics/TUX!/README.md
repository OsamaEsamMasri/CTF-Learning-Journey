# Tux!

<img width="665" height="376" alt="image" src="https://github.com/user-attachments/assets/44f4225c-0ea3-4ed7-b179-a2275787459f" />

---

## Platform
CTFLearn

## Category
Forensics

## Difficulty
Easy

---

# Challenge Description

The challenge hinted that the flag was hidden inside a penguin image using steganography techniques.

<img width="198" height="218" alt="image" src="https://github.com/user-attachments/assets/82098318-e6d0-4cf9-9ce7-9f188b1541af" />

---

# Objective

Analyze the image file and recover the hidden flag.

---

# Step 1 - Downloading the Challenge File

First, I downloaded the challenge image using `wget`:

```bash
wget https://ctflearn.com/challenge/download/973
```

After downloading the file, it was saved as:

```text
973
```

<img width="1110" height="216" alt="image" src="https://github.com/user-attachments/assets/7b4fca6f-c3c1-476f-a05e-89a40fc39d63" />

---

# Step 2 - Identifying the File Type

Next, I checked the actual file type using the `file` command:

```bash
file 973
```

Output:

```text
JPEG image data, JFIF standard 1.01
```

This confirmed that the downloaded file was actually a JPEG image.

<img width="1112" height="74" alt="image" src="https://github.com/user-attachments/assets/b0c9754b-eb95-40ff-bcb1-41c72405493a" />

---

# Step 3 - Inspecting Metadata

I used `exiftool` to inspect the image metadata:

```bash
exiftool 973
```

During the metadata analysis, I discovered a suspicious encoded comment:

```text
ICAgICAgUGFzc3dvcmQ6IExpbnV4MTIzNDUK
```

The text appeared to be Base64 encoded.

<img width="615" height="428" alt="image" src="https://github.com/user-attachments/assets/34233c18-00b3-4bf4-a490-b0c0674df0ea" />

---

# Step 4 - Decoding the Hidden Message

I decoded the Base64 string using:

```bash
echo "ICAgICAgUGFzc3dvcmQ6IExpbnV4MTIzNDUK" | base64 -d
```

The decoded message revealed:

```text
Password: Linux12345
```

This suggested that hidden content inside the image was protected with a password.

<img width="557" height="76" alt="image" src="https://github.com/user-attachments/assets/b10d1764-c515-45e0-a750-31ab24ce6def" />

---

# Step 5 - Testing Steganography Extraction

Since the challenge hinted that the flag was hidden inside the image, I attempted to extract hidden data using `steghide`:

```bash
steghide --extract -sf 973
```

However, the extraction failed and returned the following message:

```text
steghide: could not open the file "973".
```

This indicated that the hidden data was not directly extractable using `steghide`, so further forensic investigation was required.


<img width="368" height="78" alt="image" src="https://github.com/user-attachments/assets/94dc13be-2467-400a-9f6e-1c5327d3cedd" />


---

# Step 6 - Extracting Hidden Files

Next, I used `binwalk` to search for hidden embedded files inside the image:

```bash
binwalk -e 973
```

The output revealed an encrypted ZIP archive hidden inside the image.

```text
Zip archive data, encrypted
```

A new extracted directory was created:

```text
_973.extracted
```

Inside the extracted directory, I found:

```text
1570.zip
```

<img width="1448" height="362" alt="image" src="https://github.com/user-attachments/assets/63182f31-7749-4c2e-823e-0f4855baf519" />

---

# Step 7 - Extracting the ZIP Archive

I entered the extracted directory:

```bash
cd _973.extracted
```

Then I extracted the ZIP archive:

```bash
unzip 1570.zip
```

The archive requested a password.

I used the password discovered earlier from the Base64 decoded metadata:

```text
Linux12345
```

After entering the correct password, the ZIP archive extracted successfully.

<img width="528" height="126" alt="image" src="https://github.com/user-attachments/assets/cd4c138d-4313-4f57-baac-71328147122e" />

---

# Step 8 - Recovering the Flag

After extraction, a file named `flag` appeared.

I displayed its contents using:

```bash
cat flag
```

The flag was:

```text
CTFlearn{Linux_Is_Awesome}
```

<img width="438" height="63" alt="image" src="https://github.com/user-attachments/assets/7fc8b92a-af14-4b09-8691-f400441c98fc" />

---

# Flag

```text
CTFlearn{Linux_Is_Awesome}
```

---

# Tools Used

- wget
- file
- exiftool
- base64
- steghide
- binwalk
- unzip
- cat

---

# What I Learned

- How to inspect image metadata
- Detecting Base64 encoded information
- Decoding hidden messages using Base64
- Using `binwalk` to locate embedded archives
- Extracting password-protected ZIP files
- Basic steganography investigation techniques

---

# Skills Practiced

- Metadata analysis
- Base64 decoding
- Hidden archive extraction
- Linux file investigation
- Digital forensics workflow
