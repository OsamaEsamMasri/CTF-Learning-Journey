# POST Practice
<img width="670" height="333" alt="لقطة شاشة 2026-05-09 182214" src="https://github.com/user-attachments/assets/29d3d272-522d-41fb-9f85-152dae07dcb0" />
## Platform
CTFLearn

## Category
Web

## Difficulty
Medium
<img width="1915" height="918" alt="image" src="https://github.com/user-attachments/assets/5ea7bb6c-529d-4f17-aec8-6915f02b8eaf" />

---

# Challenge Description

The challenge stated that the website uses HTTP POST requests for authentication.

Although the webpage appeared incomplete, the backend functionality was still active.

---

# Objective

Authenticate to the website using POST requests and retrieve the hidden flag.

---

# Step 1 - Visiting the Website

First, I opened the target webpage in the browser:

```text
http://165.227.106.113/post.php
```

The webpage displayed the following message:

```text
This site takes POST data that you have not submitted!
```

This indicated that the application expected data through an HTTP POST request.

<img width="1272" height="720" alt="image" src="YOUR_IMAGE_LINK_HERE" />

---

# Step 2 - Inspecting the Page Source

I inspected the page source using:

```text
Ctrl + U
```

Inside the HTML source code, I discovered a hidden comment containing login credentials:

```html
<!--username: admin | password: 71urlkufpsdnlkadsf-->
```

This revealed both the username and password needed for authentication.

<img width="1272" height="720" alt="image" src="YOUR_IMAGE_LINK_HERE" />

---

# Step 3 - Sending a POST Request with curl

Since the challenge specifically required POST authentication, I used `curl` to manually send the credentials to the server:

```bash
curl -v -d "username=admin&password=71urlkufpsdnlkadsf" http://165.227.106.113/post.php
```

Explanation:

- `-d` sends POST data
- `-v` enables verbose output for inspecting the HTTP request and response

---

# Step 4 - Receiving the Flag

After sending the correct POST request, the server responded with the hidden flag:

```text
flag{p0st_d4ta_4ll_d4y}
```

<img width="1272" height="720" alt="image" src="YOUR_IMAGE_LINK_HERE" />

---

# Flag

```text
flag{p0st_d4ta_4ll_d4y}
```

---

# Tools Used

- Firefox Developer Tools
- curl

---

# What I Learned

- Difference between GET and POST requests
- How web applications handle POST authentication
- How to inspect HTML source code for hidden information
- Using `curl` to manually send POST requests
- Basic web challenge enumeration techniques

---

# Skills Practiced

- Web reconnaissance
- Source code inspection
- HTTP POST requests
- Manual authentication testing
- Linux command-line web interaction
