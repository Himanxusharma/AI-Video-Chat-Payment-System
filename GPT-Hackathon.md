# 💬💳 Live Video Payment Integration (Hackathon MVP)

## 🚀 Vision

Enable users to make secure payments during live video interactions. Perfect for telemedicine, tutoring, or consulting — where users can instantly pay during the session.

---

## 🧠 Use Cases

- **Telemedicine** – Patients pay doctors during video consultations.
- **Tutoring** – Students pay teachers per session.
- **Consulting** – Legal/financial advice with instant payment.
- **Retail Demos** – Agents show products, users buy live.
- **Real Estate** – Pay booking fees during a live virtual tour.

---

## 🧱 Tech Stack

| Layer        | Tech                          |
|--------------|-------------------------------|
| Frontend     | React + Tailwind              |
| Video        | Twilio Video / WebRTC         |
| Backend      | Node.js + Express             |
| Payment      | Razorpay / Stripe             |
| Deployment   | Vercel (frontend), Render/Heroku (backend) |

---

## 📆 Hackathon Timeline (2.5 Days)

### 🟢 Day 1 – Setup & Core Functionality (8–10 hrs)

| Time      | Task                                                   |
|-----------|--------------------------------------------------------|
| 0–2 hrs   | Project setup, Git repo, directory structure           |
| 2–5 hrs   | Integrate Twilio Video SDK or WebRTC basic P2P         |
| 5–7 hrs   | Setup backend (Express), create dummy user roles       |
| 7–9 hrs   | Create Razorpay payment link API (`/create-payment`)   |
| 9–10 hrs  | Test full round-trip: agent triggers → user sees link  |

---

### 🟡 Day 2 – Payment Integration & Real-Time Sync (10–12 hrs)

| Time      | Task                                                    |
|-----------|---------------------------------------------------------|
| 0–2 hrs   | Build UI: agent can trigger payment from video screen   |
| 2–5 hrs   | Show Razorpay modal or link inside the video/chat view |
| 5–7 hrs   | Setup webhook on backend: Razorpay → confirm payment    |
| 7–8 hrs   | Push real-time status to video UI using WebSocket/SSE   |
| 8–10 hrs  | Add payment confirmation view + success alert           |
| 10–12 hrs | Polish UI, improve UX (loading spinners, error states)  |

---

### 🟣 Day 3 (Half Day) – Polish & Deploy (4–5 hrs)

| Time      | Task                                                   |
|-----------|--------------------------------------------------------|
| 0–2 hrs   | Add session logs / invoice info / optional login       |
| 2–3 hrs   | Deploy frontend (Vercel) and backend (Render/Heroku)   |
| 3–4 hrs   | Final testing, record demo video, write presentation   |
| 4–5 hrs   | Submit, rest, celebrate 🎉                              |

---

## ⚙️ Feature Summary

| Feature                     | Status    |
|-----------------------------|-----------|
| Join live video             | ✅ Day 1  |
| Agent triggers payment link | ✅ Day 1  |
| User pays via Razorpay      | ✅ Day 2  |
| Payment confirmation        | ✅ Day 2  |
| Basic deployment            | ✅ Day 3  |

---

## 🔐 Security & Compliance

- E2E video encryption (Twilio/WebRTC)
- Razorpay tokenized + PCI-compliant
- OAuth2 or basic token auth
- Webhook signature verification
- GDPR compliance if storing personal info

---

## 🛠️ API Sample – Create Razorpay Link

```js
const Razorpay = require('razorpay');

const razorpay = new Razorpay({
  key_id: process.env.RAZORPAY_KEY,
  key_secret: process.env.RAZORPAY_SECRET
});

app.post('/create-payment-link', async (req, res) => {
  const payment = await razorpay.paymentLink.create({
    amount: 100000, // ₹1000
    currency: "INR",
    description: "Live session fee",
    callback_url: "https://yourdomain.com/payment-success",
    callback_method: "get"
  });
  res.json({ url: payment.short_url });
});
