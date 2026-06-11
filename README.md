# ⚽ Burdwan Turf — Real Client Turf Booking Platform

A production-grade MERN booking platform built for a real paying client — handled the full lifecycle from proposal, design demo, and phased billing to deployment. Users can browse available slots and book online or pay at venue; the owner manages everything through a separate secured dashboard.

**Live:** https://burdwan-turf.vercel.app

---

## Code Architecture

- user site → https://github.com/Saikat-github/burdwan-turf-frontend
- backend → confidential, can't make it public

---

## Features

### User Side
- **Browse & book slots** — view available time slots in real time
- **Dual payment flow** — pay online via Razorpay gateway or choose pay-at-venue option
- **Email confirmation** — booking confirmation sent via Resend after successful payment
- **Bot protection** — rate limiting on booking endpoints to prevent abuse

### Owner Dashboard
- **Secured access** — JWT-based auth, completely separate from the user-facing site
- **Booking management** — view all upcoming and past bookings
- **Block slots** — manually block specific time slots (maintenance, private events)
- **Configure opening hours** — set and update daily availability from the dashboard

---

## Tech Stack

| Layer | Tech |
|---|---|
| Frontend | React, TailwindCSS, React Hook Form |
| Backend | Node.js, Express.js |
| Database | MongoDB, Mongoose |
| Auth | JWT (owner dashboard) |
| Payments | Razorpay (dual flow — online + pay-at-venue) |
| Email | Resend |
| Security | express-rate-limit, express-validator |

---

## Key Implementation Highlights

- **Race condition prevention** — slot booking uses MongoDB atomic `findOneAndUpdate` with `$inc`; concurrent requests cannot double-book the same slot
- **Dual payment architecture** — online flow triggers Razorpay checkout and verifies payment via HMAC webhook before confirming booking; pay-at-venue flow bypasses gateway but still creates a pending booking record
- **RBAC** — owner dashboard routes are fully separated and protected with JWT middleware; no shared auth surface with the user panel
- **Webhook security** — Razorpay webhook payloads verified using `crypto.createHmac` before any booking state is mutated
- **Input hardening** — all user inputs validated server-side with `express-validator`; rate limiter prevents brute-force on booking and auth endpoints

---

## Screenshots


<img width="1344" height="593" alt="burdwanturf-pic-1" src="https://github.com/user-attachments/assets/c5839b87-0cb7-4e4a-a999-afb1a3729fcd" />
<img width="1341" height="592" alt="burdwanturf-pic-2" src="https://github.com/user-attachments/assets/0605aab6-ed72-428a-a244-4d19f04688af" />
<img width="1341" height="592" alt="burdwanturf-pic-3" src="https://github.com/user-attachments/assets/3616a946-4764-421c-8180-ccc368579e31" />

