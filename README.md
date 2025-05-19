<p align="center">
  <img src="https://logos-world.net/wp-content/uploads/2024/10/Bkash-Logo.jpg" height="220" />
</p>

<h1 align="center">bKash Payment Integration</h1>
<p align="center">A simple guide to integrate and test bKash payments in your Django DRF project.</p>

---

### 🚀 Quick Setup (5–10 minutes)

---

### 📁 1. Clone the Repository

```bash
git clone https://github.com/zero-byte-git/Bkash-API.git
cd Bkash-API
```

---

### 🐍 2. Create a Virtual Environment

| OS        | Command                  |
|-----------|---------------------------|
| Windows   | `python -m venv env`      |
| Linux/Mac | `python3 -m venv env`     |

---

### ⚡ 3. Activate the Environment

| OS        | Command                    |
|-----------|-----------------------------|
| Windows   | `env\Scripts\activate`      |
| Linux/Mac | `source env/bin/activate`   |

---

### 📦 4. Install Dependencies

```bash
pip install -r requirements.txt
```

---

### 🔐 5. Setup Environment Variables

1. Create a `.env` file in the project root.
2. Add your credentials:

```env
BKASH_APP_KEY=your_app_key
BKASH_APP_SECRET=your_app_secret
BKASH_USERNAME=your_username
BKASH_PASSWORD=your_password
BKASH_BASE_URL=https://tokenized.sandbox.bka.sh/v1.2.0-beta
BKASH_CALLBACK_URL=https://<your-ngrok-url>/payment/callback/
```

> ⚠️ **Note:** If you're using [ngrok](https://ngrok.com/) for local testing, make sure to update the callback URL when your ngrok address changes.

---

### 📬 6. Create a Payment (via Postman)

**Endpoint:**  
`POST http://127.0.0.1:8000/payment/create/`

**Sample Request:**
```json
{
  "amount": "50.00",
  "invoice": "INV-1006"
}
```

**Sample Response:**
```json
{
  "paymentID": "TR0011RsjP3mX1747579752377",
  "bkashURL": "https://sandbox.payment.bkash.com/?paymentId=...",
  "callbackURL": "https://<your-ngrok-url>/payment/callback/",
  ...
  "amount": "50.00",
  "transactionStatus": "Initiated",
  "statusCode": "0000",
  "statusMessage": "Successful"
}
```

---

### 🌐 7. Complete Payment in Browser

1. Copy the `bkashURL` from the response.
2. Open it in your browser.
3. Follow the steps:
   - Enter phone number and OTP.
   - Enter PIN (Sandbox PIN phase may fail—this is expected behavior).

---

### ✅ 8. Execute the Payment

**Endpoint:**  
`POST http://127.0.0.1:8000/payment/execute/`

**Sample Request:**
```json
{
  "paymentID": "TR0011RsjP3mX1747579752377"
}
```

---
