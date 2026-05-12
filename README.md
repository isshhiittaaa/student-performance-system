# AI-Powered Student Analytics Platform

A scalable MERN-based education platform backend built using Node.js, Express, and MongoDB that supports role-based authentication, quiz management, student performance tracking, and analytics-driven dashboards.

This project was designed to simulate a modern EdTech platform where teachers can manage courses and assessments while students can track progress through interactive dashboards and quiz analytics.

---

## Features

### Authentication & Authorization

* JWT-based authentication
* Secure login and registration
* Role-based access control for students and teachers
* Protected API routes using middleware

### Course & Quiz Management

* Teachers can create and manage courses
* Dynamic quiz creation with multiple questions
* Quiz scheduling using start/end timings
* Draft and publish workflow for quizzes

### Student Dashboard

* View enrolled courses
* Attempt quizzes with scoring system
* Track quiz history and performance
* Receive detailed feedback after attempts

### Teacher Dashboard

* Monitor student performance
* Access analytics for quizzes and attempts
* View leaderboard rankings and participation stats

### Analytics & Performance Tracking

* Quiz-wise leaderboard
* Global ranking system
* Student performance monitoring
* Attempt history and score analysis

---

## Tech Stack

| Layer          | Technology          |
| -------------- | ------------------- |
| Backend        | Node.js, Express.js |
| Database       | MongoDB, Mongoose   |
| Authentication | JWT                 |
| Testing        | Postman             |
| Email Service  | Nodemailer          |

---

## Project Structure

```bash
controllers/
middleware/
models/
routes/
config/
utils/
server.js
```

---

## API Modules

* Authentication APIs
* Course Management APIs
* Quiz Management APIs
* Dashboard & Analytics APIs
* Leaderboard APIs

---

## Future Improvements

* AI-powered student performance prediction
* Personalized quiz recommendations
* Real-time notifications
* Certificate verification system
* Frontend integration using React/Next.js
* Advanced analytics dashboard

---

## Installation

```bash
npm install
npm run dev
```

---

## Learning Outcomes

* REST API architecture
* Authentication & authorization
* Middleware-based security
* MongoDB schema design
* Role-based backend systems
* Scalable backend development

---

## Author

Developed by Ishita Srivastava
