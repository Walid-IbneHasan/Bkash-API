# bKash Payment Integration: Quick Start Guide

Welcome! This guide will help you set up and test the bKash payment flow in your local environment.
**Estimated setup time:** 5-10 minutes

---

## 1️⃣ Clone the Repository

```bash
git clone [https://github.com/zero-byte-git/Bkash-API.git](https://github.com/zero-byte-git/Bkash-API.git)
```bash
cd Bkash-API
2️⃣ Create a Python Virtual EnvironmentPlatformCommand🪟 Windowspython -m venv env🐧 Linuxpython3 -m venv env3️⃣ Activate the EnvironmentPlatformCommand🪟 Windowsenv\Scripts\activate🐧 Linuxsource env/bin/activate4️⃣ Install Project Dependenciespip install -r requirements.txt
5️⃣ Configure Environment VariablesCreate a .env file in your project root.Add the following (replace placeholders with your credentials):BKASH_APP_KEY=your_app_key
BKASH_APP_SECRET=your_app_secret
BKASH_USERNAME=your_username
BKASH_PASSWORD=your_password
BKASH_BASE_URL=https://tokenized.sandbox.bka.sh/v1.2.0-beta
BKASH_CALLBACK_URL=https://740e-118-179-44-184.ngrok-free.app/payment/callback/
⚠️ Note:This example uses ngrok for local callback URLs.Update the callback URL if your ngrok address changes.6️⃣ Initiate a Payment (Using Postman)Endpoint:POST http://127.0.0.1:8000/payment/create/Request Body:{
  "amount": "50.00",
  "invoice": "INV-1006"
}
Sample Success Response:{
  "paymentID": "TR0011RsjP3mX1747579752377",
  "bkashURL": "https://sandbox.payment.bkash.com/?paymentId=TR0011RsjP3mX1747579752377&hash=...&mode=0011&apiVersion=v1.2.0-beta/",
  "callbackURL": "https://740e-118-179-44-184.ngrok-free.app/payment/callback/",
  "successCallbackURL": "...",
  "failureCallbackURL": "...",
  "cancelledCallbackURL": "...",
  "amount": "50.00",
  "intent": "sale",
  "currency": "BDT",
  "paymentCreateTime": "2025-05-18T20:49:12:377 GMT+0600",
  "transactionStatus": "Initiated",
  "merchantInvoiceNumber": "INV-1005",
  "statusCode": "0000",
  "statusMessage": "Successful"
}
7️⃣ Complete the Payment in BrowserCopy the bkashURL from the response.Open it in your browser.Follow the payment steps:    - Enter phone number and OTP (should succeed).    - Enter PIN (sandbox may fail here; this is expected).8️⃣ Execute the PaymentEndpoint:POST http://127.0.0.1:8000/payment/execute/Request Body:{
  "paymentID": "TR0011RsjP3mX1747579752377"
}
