# 🎯 FastAPI QR Code Generator Project

This is my mini project using **FastAPI** where I built an API that can:

- Let you **log in**
- Let logged-in users **generate QR codes** with custom colors and size
- Let users **delete** QR codes they made
- Has proper **login security** using tokens (JWT)
- Also has a **test file** that checks if all things are working
- CI/CD setup with GitHub Actions to auto-test code on every push

---

## 💻 Tech Used

- FastAPI (main backend framework)
- Python JWT (token-based login)
- qrcode + Pillow (for QR code images)
- HTTPX + Pytest (for testing)
- GitHub Actions (for auto-testing when code is pushed)

---

## 🚀 How to Run

### Step 1: Install requirements

```bash
pip install -r requirements.txt
```

If Pillow error comes (like `No module named 'PIL'`), just install it separately:

```bash
pip install Pillow
```

### Step 2: Run the API

```bash
uvicorn app.main:app --reload
```

Then go to [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs) to test the API easily using Swagger UI.

---

## 🔐 Login First (Important)

Before using QR generator, you must login.

### Endpoint: `/token`

Use these values:
```json
{
  "username": "admin",
  "password": "secret"
}
```

It will give you a token like:
```json
{
  "access_token": "abcd1234",
  "token_type": "bearer"
}
```

---

## 🧾 How to Use API (after login)

### 1. Generate QR Code

**POST `/qr-codes/`**

Add this in headers:
```
Authorization: Bearer <your_token>
```

Example body:
```json
{
  "url": "https://example.com",
  "fill_color": "blue",
  "back_color": "white",
  "size": 10
}
```

Response will return the URL to the QR image.

---

### 2. Delete QR Code

**DELETE `/qr-codes/{filename}`**

You can copy filename from the QR image URL you got earlier. Add the same token in header.

---

## ✅ How I Tested

I made a test file: `tests/start_test.py`

It checks:
- Login works
- If someone tries QR creation without login, it fails
- If login is done, it can generate and delete QR

To run tests:

```bash
pytest
```

---

## 🔁 GitHub Actions Setup (Auto-Test)

When I push my code to GitHub, it automatically runs tests using GitHub Actions.

It:
- Installs Python
- Installs requirements
- Runs tests

If tests pass, green tick ✅  
If anything fails, red cross ❌

---
