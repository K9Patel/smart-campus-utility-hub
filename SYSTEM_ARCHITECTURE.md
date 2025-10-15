# 🏗️ SMART CAMPUS - SYSTEM ARCHITECTURE

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                        🌐 USER INTERFACE (Browser)                           │
│                         http://localhost:5174                                │
└───────────────────────────────┬──────────────────────────────────────────────┘
                                │
                                │ HTTPS/HTTP
                                │
┌───────────────────────────────▼──────────────────────────────────────────────┐
│                                                                              │
│                     ⚛️  SMART CAMPUS FRONTEND                                │
│                      React 18 + Vite 7 + Tailwind CSS                        │
│                                                                              │
│  ┌────────────────────────────────────────────────────────────────────────┐ │
│  │                         📱 PAGES LAYER                                  │ │
│  │  ┌─────────────┬─────────────┬─────────────┬────────────┬────────────┐ │ │
│  │  │ Landing     │ Login       │ Dashboard   │ Events     │ Timetable  │ │ │
│  │  │ Register    │ Profile     │ Settings    │ Electives  │            │ │ │
│  │  └─────────────┴─────────────┴─────────────┴────────────┴────────────┘ │ │
│  └────────────────────────────────────────────────────────────────────────┘ │
│                                    ↕                                         │
│  ┌────────────────────────────────────────────────────────────────────────┐ │
│  │                    🎨 COMPONENTS LAYER                                  │ │
│  │  ┌────────────┬────────────┬────────────┬────────────┬─────────────┐  │ │
│  │  │ Navbar     │ Sidebar    │ Button     │ Input      │ Card        │  │ │
│  │  │ Footer     │ EventCard  │ Modal      │ Skeleton   │ Animation   │  │ │
│  │  └────────────┴────────────┴────────────┴────────────┴─────────────┘  │ │
│  └────────────────────────────────────────────────────────────────────────┘ │
│                                    ↕                                         │
│  ┌────────────────────────────────────────────────────────────────────────┐ │
│  │                    🔧 STATE MANAGEMENT                                  │ │
│  │  ┌──────────────────────┬──────────────────────┬───────────────────┐  │ │
│  │  │  Zustand (Auth)      │  React Query (API)   │  React Context    │  │ │
│  │  │  • User State        │  • Server Cache      │  • Theme          │  │ │
│  │  │  • Login/Logout      │  • Auto Refetch      │  • Dark/Light     │  │ │
│  │  └──────────────────────┴──────────────────────┴───────────────────┘  │ │
│  └────────────────────────────────────────────────────────────────────────┘ │
│                                    ↕                                         │
│  ┌────────────────────────────────────────────────────────────────────────┐ │
│  │                    📡 API SERVICE LAYER (src/lib/api.js)                │ │
│  │  ┌──────────────────────────────────────────────────────────────────┐  │ │
│  │  │  Axios Client + Interceptors                                     │  │ │
│  │  │  • Base URL: http://localhost:5000/api                           │  │ │
│  │  │  • Request: Auto-attach JWT token                                │  │ │
│  │  │  • Response: Handle 401, 403, 404, 500 errors                    │  │ │
│  │  └──────────────────────────────────────────────────────────────────┘  │ │
│  │  ┌──────────────────────────────────────────────────────────────────┐  │ │
│  │  │  📋 Service Modules                                               │  │ │
│  │  │  • authService       - Login, Register, Profile                  │  │ │
│  │  │  • eventService      - Events CRUD, Save/Unsave                  │  │ │
│  │  │  • clubService       - Clubs listing                             │  │ │
│  │  │  • electiveService   - Electives, Submit choices, Allocation     │  │ │
│  │  │  • timetableService  - Group/Teacher timetables                  │  │ │
│  │  └──────────────────────────────────────────────────────────────────┘  │ │
│  └────────────────────────────────────────────────────────────────────────┘ │
│                                                                              │
└───────────────────────────────┬──────────────────────────────────────────────┘
                                │
                                │ REST API (JSON)
                                │ JWT Authentication
                                │
┌───────────────────────────────▼──────────────────────────────────────────────┐
│                                                                              │
│                     🚀 SMART CAMPUS BACKEND                                  │
│                  Node.js 18 + Express 5 + PostgreSQL 14                      │
│                         http://localhost:5000                                │
│                                                                              │
│  ┌────────────────────────────────────────────────────────────────────────┐ │
│  │                    🛡️  MIDDLEWARE LAYER                                 │ │
│  │  ┌──────────────┬──────────────┬──────────────┬────────────────────┐  │ │
│  │  │ CORS         │ Helmet       │ Rate Limiter │ Compression        │  │ │
│  │  │ (Origins)    │ (Security)   │ (100/15min)  │ (gzip)             │  │ │
│  │  └──────────────┴──────────────┴──────────────┴────────────────────┘  │ │
│  │  ┌──────────────┬──────────────┬──────────────┬────────────────────┐  │ │
│  │  │ Auth         │ Validation   │ Error        │ Logger             │  │ │
│  │  │ (JWT Verify) │ (Joi)        │ Handler      │ (Winston)          │  │ │
│  │  └──────────────┴──────────────┴──────────────┴────────────────────┘  │ │
│  └────────────────────────────────────────────────────────────────────────┘ │
│                                    ↕                                         │
│  ┌────────────────────────────────────────────────────────────────────────┐ │
│  │                    🛣️  API ROUTES                                       │ │
│  │                                                                         │ │
│  │  POST   /api/auth/register       ─┐                                    │ │
│  │  POST   /api/auth/login           │  Authentication                    │ │
│  │  GET    /api/auth/profile         │                                    │ │
│  │  PUT    /api/auth/profile        ─┘                                    │ │
│  │                                                                         │ │
│  │  GET    /api/events              ─┐                                    │ │
│  │  GET    /api/events/:id           │  Campus Events                     │ │
│  │  POST   /api/events/:id/save      │                                    │ │
│  │  GET    /api/events/saved        ─┘                                    │ │
│  │                                                                         │ │
│  │  GET    /api/clubs               ─┐                                    │ │
│  │  GET    /api/clubs/:id           ─┘  Clubs                             │ │
│  │                                                                         │ │
│  │  GET    /api/timetable/group/:id ─┐                                    │ │
│  │  GET    /api/timetable/teacher/:id┘  Timetable                         │ │
│  │                                                                         │ │
│  │  GET    /api/electives           ─┐                                    │ │
│  │  POST   /api/electives/choices    │  Electives                         │ │
│  │  GET    /api/electives/my/allocation─┘                                 │ │
│  │                                                                         │ │
│  └────────────────────────────────────────────────────────────────────────┘ │
│                                    ↕                                         │
│  ┌────────────────────────────────────────────────────────────────────────┐ │
│  │                    🎯 CONTROLLERS                                       │ │
│  │  ┌───────────────┬───────────────┬───────────────┬──────────────────┐ │ │
│  │  │ user.         │ events.       │ timetable.    │ elective.        │ │ │
│  │  │ controller.js │ controller.js │ controller.js │ controller.js    │ │ │
│  │  │               │ clubs.        │               │                  │ │ │
│  │  │               │ controller.js │               │                  │ │ │
│  │  └───────────────┴───────────────┴───────────────┴──────────────────┘ │ │
│  │  • Business Logic                                                      │ │
│  │  • Input Validation (Joi)                                              │ │
│  │  • JWT Token Generation/Verification                                   │ │
│  │  • Password Hashing (bcrypt)                                           │ │
│  └────────────────────────────────────────────────────────────────────────┘ │
│                                    ↕                                         │
│  ┌────────────────────────────────────────────────────────────────────────┐ │
│  │                    🗄️  DATABASE CONNECTION                              │ │
│  │  ┌──────────────────────────────────────────────────────────────────┐ │ │
│  │  │  pg (node-postgres)                                               │ │ │
│  │  │  • Connection Pool (min: 2, max: 10)                              │ │ │
│  │  │  • Parameterized Queries (SQL Injection Prevention)               │ │ │
│  │  │  • Transaction Support                                            │ │ │
│  │  └──────────────────────────────────────────────────────────────────┘ │ │
│  └────────────────────────────────────────────────────────────────────────┘ │
│                                                                              │
└───────────────────────────────┬──────────────────────────────────────────────┘
                                │
                                │ SQL Queries
                                │
┌───────────────────────────────▼──────────────────────────────────────────────┐
│                                                                              │
│                     🗄️  POSTGRESQL DATABASE                                  │
│                      smart_campus_unified (Port 5432)                        │
│                                                                              │
│  ┌────────────────────────────────────────────────────────────────────────┐ │
│  │                    📊 DATABASE TABLES (15 Total)                        │ │
│  │                                                                         │ │
│  │  🔐 AUTHENTICATION MODULE                                               │ │
│  │  ┌──────────────────────────────────────────────────────────────────┐ │ │
│  │  │  users                                                            │ │ │
│  │  │  • id, full_name, email, password_hash, role                     │ │ │
│  │  │  • department, cgpa, semester                                    │ │ │
│  │  └──────────────────────────────────────────────────────────────────┘ │ │
│  │                                                                         │ │
│  │  🎉 CAMPUS EVENTS MODULE                                                │ │
│  │  ┌──────────────────────────────────────────────────────────────────┐ │ │
│  │  │  clubs                                                            │ │ │
│  │  │  • id, name, description, category                               │ │ │
│  │  ├──────────────────────────────────────────────────────────────────┤ │ │
│  │  │  events                                                           │ │ │
│  │  │  • id, title, location, start_time, end_time, club_id            │ │ │
│  │  ├──────────────────────────────────────────────────────────────────┤ │ │
│  │  │  saved_events (Many-to-Many)                                     │ │ │
│  │  │  • user_id, event_id, saved_at                                   │ │ │
│  │  └──────────────────────────────────────────────────────────────────┘ │ │
│  │                                                                         │ │
│  │  🎯 ELECTIVES MODULE                                                    │ │
│  │  ┌──────────────────────────────────────────────────────────────────┐ │ │
│  │  │  electives                                                        │ │ │
│  │  │  • id, subject_name, max_students, semester                      │ │ │
│  │  ├──────────────────────────────────────────────────────────────────┤ │ │
│  │  │  student_choices                                                 │ │ │
│  │  │  • id, student_id, elective_id, preference_rank                  │ │ │
│  │  ├──────────────────────────────────────────────────────────────────┤ │ │
│  │  │  allocated_electives                                             │ │ │
│  │  │  • id, student_id, elective_id, allocated_at                     │ │ │
│  │  └──────────────────────────────────────────────────────────────────┘ │ │
│  │                                                                         │ │
│  │  📅 TIMETABLE MODULE                                                    │ │
│  │  ┌──────────────────────────────────────────────────────────────────┐ │ │
│  │  │  teachers                                                         │ │ │
│  │  │  • id (UUID), teacher_code, full_name, department                │ │ │
│  │  ├──────────────────────────────────────────────────────────────────┤ │ │
│  │  │  subjects                                                         │ │ │
│  │  │  • id (UUID), subject_code, subject_name, hours_per_week         │ │ │
│  │  ├──────────────────────────────────────────────────────────────────┤ │ │
│  │  │  rooms                                                            │ │ │
│  │  │  • id (UUID), room_code, capacity, room_type                     │ │ │
│  │  ├──────────────────────────────────────────────────────────────────┤ │ │
│  │  │  student_groups                                                  │ │ │
│  │  │  • id (UUID), group_code, strength, semester                     │ │ │
│  │  ├──────────────────────────────────────────────────────────────────┤ │ │
│  │  │  teacher_subject_assignments (Many-to-Many)                      │ │ │
│  │  ├──────────────────────────────────────────────────────────────────┤ │ │
│  │  │  subject_class_assignments (Many-to-Many)                        │ │ │
│  │  ├──────────────────────────────────────────────────────────────────┤ │ │
│  │  │  teacher_unavailability                                          │ │ │
│  │  ├──────────────────────────────────────────────────────────────────┤ │ │
│  │  │  timetable_slots                                                 │ │ │
│  │  │  • day_of_week, period_number, teacher_id, subject_id, room_id  │ │ │
│  │  └──────────────────────────────────────────────────────────────────┘ │ │
│  │                                                                         │ │
│  │  🔗 Relationships:                                                      │ │
│  │    • Foreign Keys: 20+ constraints                                     │ │
│  │    • Indexes: 25+ for performance                                      │ │
│  │    • Triggers: Auto-update timestamps                                  │ │
│  │    • Constraints: UNIQUE, CHECK, NOT NULL                              │ │
│  │                                                                         │ │
│  └────────────────────────────────────────────────────────────────────────┘ │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


                          🔐 AUTHENTICATION FLOW


┌─────────┐         ┌─────────┐         ┌─────────┐         ┌─────────┐
│ User    │         │ React   │         │ Express │         │ PostgreSQL
│ Browser │         │ Frontend│         │ Backend │         │ Database│
└────┬────┘         └────┬────┘         └────┬────┘         └────┬────┘
     │                   │                   │                   │
     │  Enter Credentials│                   │                   │
     ├──────────────────>│                   │                   │
     │                   │  POST /api/auth/login                 │
     │                   ├──────────────────>│                   │
     │                   │  { email, pwd }   │                   │
     │                   │                   │  SELECT * FROM users
     │                   │                   ├──────────────────>│
     │                   │                   │                   │
     │                   │                   │  User record      │
     │                   │                   │<──────────────────┤
     │                   │                   │                   │
     │                   │  Verify password  │                   │
     │                   │  bcrypt.compare() │                   │
     │                   │                   │                   │
     │                   │  Generate JWT     │                   │
     │                   │  jwt.sign()       │                   │
     │                   │                   │                   │
     │                   │  { token, user }  │                   │
     │                   │<──────────────────┤                   │
     │                   │                   │                   │
     │  Store token      │                   │                   │
     │  localStorage     │                   │                   │
     │<──────────────────┤                   │                   │
     │                   │                   │                   │
     │  Navigate to /dashboard               │                   │
     │<──────────────────┤                   │                   │
     │                   │                   │                   │


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


                          📡 API REQUEST FLOW (with JWT)


┌─────────┐         ┌─────────┐         ┌─────────┐         ┌─────────┐
│ React   │         │ Axios   │         │ Express │         │ PostgreSQL
│ Component│         │Interceptor       │ API     │         │ Database│
└────┬────┘         └────┬────┘         └────┬────┘         └────┬────┘
     │                   │                   │                   │
     │  eventService.    │                   │                   │
     │  getEvents()      │                   │                   │
     ├──────────────────>│                   │                   │
     │                   │                   │                   │
     │  Request          │                   │                   │
     │  Interceptor:     │                   │                   │
     │  Add JWT token    │                   │                   │
     │  from localStorage│                   │                   │
     │                   │                   │                   │
     │                   │  GET /api/events  │                   │
     │                   │  Authorization:   │                   │
     │                   │  Bearer <token>   │                   │
     │                   ├──────────────────>│                   │
     │                   │                   │                   │
     │                   │  auth.middleware  │                   │
     │                   │  Verify JWT       │                   │
     │                   │  jwt.verify()     │                   │
     │                   │                   │                   │
     │                   │                   │  SELECT * FROM events
     │                   │                   ├──────────────────>│
     │                   │                   │                   │
     │                   │                   │  Events data      │
     │                   │                   │<──────────────────┤
     │                   │                   │                   │
     │                   │  { data: [...] }  │                   │
     │                   │<──────────────────┤                   │
     │                   │                   │                   │
     │  Response         │                   │                   │
     │  Interceptor:     │                   │                   │
     │  Extract data     │                   │                   │
     │                   │                   │                   │
     │  setEvents(data)  │                   │                   │
     │<──────────────────┤                   │                   │
     │                   │                   │                   │
     │  Re-render with   │                   │                   │
     │  new data         │                   │                   │
     │                   │                   │                   │


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


                          ⚡ TECHNOLOGY STACK DETAILS


┌────────────────────────────────────────────────────────────────────────────┐
│  FRONTEND STACK                                                            │
├────────────────────────────────────────────────────────────────────────────┤
│  Framework         │  React 18.3.1                                         │
│  Build Tool        │  Vite 7.1.9 (Lightning-fast HMR)                     │
│  Styling           │  Tailwind CSS 3.4+ (Utility-first)                   │
│  Animations        │  Framer Motion 11.15+ (Production-ready)             │
│  State (Auth)      │  Zustand 5.0.2 (Lightweight, 1.2KB)                  │
│  State (Server)    │  React Query 5.62+ (Auto cache & refetch)            │
│  Routing           │  React Router v7.1.4 (SPA routing)                   │
│  HTTP Client       │  Axios 1.7.9 (Interceptors, error handling)          │
│  Forms             │  React Hook Form + Zod (Validation)                  │
│  Icons             │  Lucide React (Beautiful icons)                      │
│  Notifications     │  React Hot Toast (Toast messages)                    │
│  Charts            │  Recharts (Data visualization)                       │
│  Testing           │  Vitest 3.x + React Testing Library                  │
│  Date Handling     │  date-fns (Modern date utility)                      │
└────────────────────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────────────────────────┐
│  BACKEND STACK                                                             │
├────────────────────────────────────────────────────────────────────────────┤
│  Runtime           │  Node.js 18+ (LTS)                                    │
│  Framework         │  Express 5.1.0 (Fast, minimal)                       │
│  Database          │  PostgreSQL 14+ (Relational)                         │
│  DB Client         │  pg 8.16.3 (node-postgres)                           │
│  Authentication    │  jsonwebtoken 9.0.2 (JWT)                            │
│  Password Hash     │  bcryptjs 3.0.2 (Secure hashing)                     │
│  Security          │  helmet 7.1.0 (HTTP headers)                         │
│  CORS              │  cors 2.8.5 (Cross-origin)                           │
│  Rate Limiting     │  express-rate-limit 7.1.5 (DoS protection)           │
│  Validation        │  joi 17.11.0 + express-validator 7.0.1               │
│  Logging           │  winston 3.11.0 (Production logs)                    │
│  Compression       │  compression 1.7.4 (gzip)                            │
│  Testing           │  jest 29.7.0 + supertest 6.3.3                       │
│  Dev Server        │  nodemon 3.1.10 (Auto-restart)                       │
└────────────────────────────────────────────────────────────────────────────┘


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


                          ✅ INTEGRATION CHECKLIST


🔐 AUTHENTICATION
  ✅ JWT token generation
  ✅ Password hashing (bcrypt)
  ✅ Login endpoint working
  ✅ Register endpoint working
  ✅ Profile endpoint working
  ✅ Token verification middleware
  ✅ Auto-logout on 401

📡 API INTEGRATION
  ✅ Axios client configured
  ✅ Request interceptor (add token)
  ✅ Response interceptor (error handling)
  ✅ authService module
  ✅ eventService module
  ✅ clubService module
  ✅ electiveService module
  ✅ timetableService module

🎉 EVENTS MODULE
  ✅ GET /api/events endpoint
  ✅ Filter by club, date, search
  ✅ Save/unsave events
  ✅ Frontend connected to API
  ✅ Loading states
  ✅ Error handling

📅 TIMETABLE MODULE
  ✅ GET /api/timetable/group/:id
  ✅ GET /api/timetable/teacher/:id
  ✅ Frontend grid rendering
  ✅ PDF export (client-side)

🎯 ELECTIVES MODULE
  ✅ GET /api/electives endpoint
  ✅ POST /api/electives/choices
  ✅ GET /api/electives/my/allocation
  ✅ Drag-and-drop UI
  ✅ Submission with confetti

🛡️ SECURITY
  ✅ CORS configured
  ✅ Rate limiting enabled
  ✅ Helmet security headers
  ✅ Input validation (Joi)
  ✅ SQL injection prevention
  ✅ Password never stored plaintext

🗄️ DATABASE
  ✅ 15 tables created
  ✅ Foreign keys configured
  ✅ Indexes for performance
  ✅ Triggers for timestamps
  ✅ Enum types defined

📚 DOCUMENTATION
  ✅ INTEGRATION_COMPLETE.md
  ✅ INTEGRATION_TESTING.md
  ✅ README.md
  ✅ This architecture diagram
  ✅ API documentation
  ✅ Database schema

🧪 TESTING
  ✅ Vitest configured
  ✅ 31/46 frontend tests passing
  ✅ Backend test suite available
  ⏳ Integration tests to be run


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Status: ✅ FULLY INTEGRATED & READY FOR TESTING
Next Step: Run integration tests → Deploy to production
```
