🎓 Student Performance System — Education & Quiz Platform Backend

A production-grade, API-first learning platform with JWT auth, role-based access, real-time quiz engine, automated email reports, dynamic leaderboards, and certificate generation.


🚀 Overview
Student Performance System is a scalable backend built with Node.js, Express, and MongoDB that powers an interactive education platform. It supports two roles — students and teachers — with fully isolated dashboards, timed quiz workflows, performance tracking, and automated email delivery.
Built end-to-end: from database schema design and REST API architecture to middleware-based authorization, email automation, and certificate generation logic.

✨ Key Features
🔐 Authentication & Authorization

Secure JWT-based registration and login
Role-based access control (RBAC) enforced via middleware — student vs. teacher routes are fully isolated
Token validation on every protected route

📚 Course Management

Teachers can create and manage courses
Students can enroll in courses via authenticated API calls
Role-aware course listing — teachers see all, students see only enrolled

❓ Quiz Engine

Teachers create quizzes with any number of questions, linked to specific courses
Draft / Publish visibility control
Time-windowed quizzes — students are blocked from attempting outside the set startTime / endTime
One attempt per student — enforced server-side, not client-side
Immediate per-question feedback (correct/wrong) on submission
Automated email report sent to student after every attempt via Nodemailer + Gmail SMTP
Certificate generation if student crosses passing threshold 🎓

🏆 Leaderboards

Quiz-specific leaderboard — ranked by score and completion time
Global leaderboard — aggregated across all quizzes platform-wide

📊 Student Dashboard

View enrolled courses, available quizzes, attempt history
Per-quiz detailed question-level feedback

📈 Teacher Dashboard

View all created courses and quiz stats (total students, attempt counts)
Access any student's full performance history — no separate login needed


🏗️ Project Structure
📦 student-performance-system
├── controllers/
│   ├── authController.js        # Registration, login, token issuance
│   ├── courseController.js      # Course CRUD, enrollment logic
│   ├── quizController.js        # Quiz lifecycle, attempt handling, scoring
│   └── dashboardController.js  # Student & teacher dashboard aggregations
│
├── middleware/
│   ├── authMiddleware.js        # JWT verification on protected routes
│   └── roleMiddleware.js        # Role guard — student vs. teacher enforcement
│
├── models/
│   ├── User.js                  # Unified user model with role field
│   ├── Course.js                # Course schema with enrollment references
│   ├── Quiz.js                  # Quiz schema: questions, visibility, time window
│   ├── QuizAttempt.js           # Attempt record: answers, score, timestamps
│   └── Certificate.js          # Certificate record with eligibility check
│
├── routes/
│   ├── authRoutes.js
│   ├── courseRoutes.js
│   ├── quizRoutes.js
│   └── dashboardRoutes.js
│
├── utils/
│   ├── tokenUtils.js            # JWT sign/verify helpers
│   └── emailSender.js           # Nodemailer SMTP integration
│
├── config/
│   └── db.js                    # MongoDB connection via Mongoose
│
└── server.js                    # Express app entry point

⚙️ Tech Stack
LayerTechnologyRuntimeNode.js (ES6+)FrameworkExpress.jsDatabaseMongoDB + Mongoose ORMAuthenticationJWT (JSON Web Tokens)AuthorizationCustom middleware (RBAC)EmailNodemailer with Gmail SMTPTestingPostman

🔌 REST API Reference
Auth
MethodRouteDescriptionPOST/api/auth/registerRegister as student or teacherPOST/api/auth/loginLogin — returns JWT + user info
Courses
MethodRouteDescriptionGET/api/coursesView all courses (filtered by role)POST/api/courses/:id/enrollStudent enrolls in a course
Quizzes
MethodRouteDescriptionPOST/api/quizzesCreate a quiz (teacher only)GET/api/quizzesList available quizzes (by role)GET/api/quizzes/:idGet a specific quizPOST/api/quizzes/:quizId/attemptSubmit quiz attemptGET/api/quizzes/:quizId/leaderboardQuiz-specific leaderboardGET/api/leaderboard/globalGlobal leaderboardGET/api/quizzes/:id/certificateDownload certificate (if eligible)
Dashboards
MethodRouteDescriptionGET/api/dashboard/studentStudent's own dashboardGET/api/dashboard/:id/studentTeacher views any student's dashboard

🔒 Authentication Flow
POST /api/auth/register  →  Create account (student/teacher)
POST /api/auth/login     →  Returns signed JWT

All subsequent requests:
  Authorization: Bearer <token>
  → authMiddleware verifies token
  → roleMiddleware checks role for restricted routes

🧪 Running Locally
bashgit clone https://github.com/isshhiittaaa/student-performance-system
cd student-performance-system
npm install
Create a .env file:
envMONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
EMAIL_USER=your_gmail@gmail.com
EMAIL_PASS=your_app_password
PORT=5000
Start the server:
bashnpm run dev
Testing with Postman

Register as both teacher and student
Teacher: Create a course → Create a quiz (set startTime, endTime, duration)
Student: Enroll in course → Attempt quiz within the time window
Verify: score response, per-question feedback, email delivery, certificate generation
Check leaderboard and dashboard routes for both roles


🗺️ Design Decisions
One attempt per student — enforced server-side
Before processing a submission, quizController.js checks QuizAttempt for an existing record matching (quizId, userId). No client-side state is trusted.
Time-windowed quizzes
The quiz model stores startTime and endTime. On each attempt request, the server compares Date.now() against the window and rejects out-of-window requests with a 403.
Role isolation via middleware factory
A single roleMiddleware accepts an array of permitted roles, keeping routes clean:
jsrouter.get('/teacher-only', authenticate, authorize(['teacher']), handler);

🔜 Planned Extensions

 Tag-based quiz filters and search
 Certificate verification via unique shareable link
 Paginated leaderboards with cursor-based pagination
 Rate limiting on quiz submission endpoints
 Unit and integration tests (Jest + Supertest)
 CI/CD pipeline with GitHub Actions


👩‍💻 Contributors

Ishita Srivastava — @isshhiittaaa
