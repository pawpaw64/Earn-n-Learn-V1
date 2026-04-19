# Earn-n-Learn

> A full-stack campus productivity platform that empowers students to earn income, share skills, trade materials, collaborate on projects, and connect with peers — all within one unified ecosystem.

## 🎥 Demo Video

[![Watch the demo](https://img.youtube.com/vi/jBf_TcsDPIE/0.jpg)](https://youtu.be/jBf_TcsDPIE)

---

## Table of Contents

1. [Project Overview](#-project-overview)
2. [Key Features](#-key-features)
3. [Technology Stack](#-technology-stack)
4. [Project Structure](#-project-structure)
5. [Setup Instructions](#-setup-instructions)
6. [API Endpoints](#-api-endpoints)
7. [Database Schema](#-database-schema)
8. [Contributing](#-contributing)
9. [License & Acknowledgments](#-license--acknowledgments)

---

## 📖 Project Overview

**Earn-n-Learn** is a campus-focused web application designed to bridge the gap between student talent and real-world opportunities. Students can post and apply for campus jobs, list skills they are willing to teach or offer as freelance services, buy and sell study materials, and collaborate on projects together — all under one roof.

The platform also features a real-time chat system (direct messages and group chats powered by Socket.IO), a Campus Hub for peer discussions, announcements, and polls, and an integrated Wallet with escrow support to ensure safe and transparent transactions between students.

**Target Users:**
- **Students** — browse jobs, offer skills, trade materials, manage projects, and chat with peers
- **Campus administrators / power users** — post announcements, manage group channels, and track project milestones

---

## ✨ Key Features

### Student-Facing Features

| Feature | Description |
|---|---|
| **Job Board** | Post and apply for campus jobs (freelance, part-time, one-time gigs). Supports cover letters, resume uploads, and application status tracking. |
| **Skills Marketplace** | List skills (tutoring, design, coding, etc.) with pricing and availability. Other students can browse and send contact requests. |
| **Materials Marketplace** | Buy and sell textbooks, notes, and equipment. Includes item condition, pricing, deadline, and image upload. |
| **Project Management** | Convert accepted job/skill applications into structured projects with milestones, tasks, time tracking, resource sharing, and activity logs. |
| **Real-Time Messaging** | Direct messages and group chats with file/media attachments (images, videos, documents), typing indicators, and live delivery via Socket.IO. |
| **Campus Hub** | Community feed supporting questions, discussions, announcements, and polls with tagging, likes, comments, and nested replies. |
| **Wallet** | In-app digital wallet supporting top-up, withdrawal, payment methods, transaction history, savings goals, and escrow-protected payments. |
| **Profile & Portfolio** | Rich user profiles with avatar, bio, university details, listed skills, portfolio items, and linked websites. |
| **Leaderboard** | Recognition system for active and high-performing campus contributors. |
| **Notifications** | In-app notification system for job applications, project updates, messages, and marketplace activity. |
| **Invoices** | Generate and manage invoices for completed work. |
| **Calendar** | Visualise deadlines, milestones, and scheduled work in a calendar view. |

### Platform-Level Features

- JWT-based authentication with protected API routes
- Escrow transaction system with dispute handling for safe peer payments
- File uploads for avatars, resumes, skill/material images, and chat attachments
- Database auto-initialisation on server start
- Concurrent frontend (Vite dev server) and backend (Express) startup via a single command

---

## 🛠 Technology Stack

### Frontend

| Technology | Purpose |
|---|---|
| **React 18** | Component-based UI framework for building a dynamic single-page application |
| **TypeScript** | Static typing for safer, more maintainable frontend code |
| **Vite** | Lightning-fast development server and optimised production build tool |
| **React Router v6** | Client-side routing for the multi-page dashboard experience |
| **Tailwind CSS** | Utility-first CSS framework for rapid, consistent styling |
| **shadcn/ui + Radix UI** | Accessible, unstyled component primitives with ready-to-use shadcn wrappers |
| **TanStack Query (React Query)** | Server-state management, caching, and background data refetching |
| **React Hook Form + Zod** | Performant form handling with schema-based validation |
| **Recharts** | Declarative charting library for financial graphs in the Wallet dashboard |
| **Socket.IO Client** | Real-time bidirectional communication for the messaging system |
| **Axios** | HTTP client for all REST API calls |
| **date-fns** | Lightweight date utility library |
| **Lucide React** | Icon set consistent with the shadcn design system |
| **Sonner** | Toast notification library |

### Backend

| Technology | Purpose |
|---|---|
| **Node.js** | JavaScript runtime for the server |
| **Express.js** | Minimal web framework providing REST API routing and middleware |
| **Socket.IO** | WebSocket-based real-time messaging (direct and group chats) |
| **MySQL 2** | Relational database driver with promise support |
| **bcryptjs** | Password hashing for secure credential storage |
| **JSON Web Tokens (JWT)** | Stateless authentication via bearer tokens |
| **Multer** | Multipart file upload handling for avatars, resumes, and chat attachments |
| **dotenv** | Environment variable management |
| **CORS** | Cross-origin resource sharing configuration |

### Database

| Technology | Purpose |
|---|---|
| **MySQL** | Primary relational database. Chosen for structured relationships between users, jobs, projects, wallets, and marketplace listings |

---

## 📁 Project Structure

```
Earn-n-Learn-V1/
├── server.js                        # Entry point — starts frontend dev server + backend concurrently
├── index.html                       # Vite HTML shell
├── package.json
├── vite.config.ts
├── tailwind.config.ts
├── tsconfig.json
├── .env                             # Environment variables (DB credentials, JWT secret, port)
├── uploads/                         # Runtime file uploads (avatars, resumes, message attachments)
│
└── src/
    ├── main.tsx                     # React app entry point
    ├── App.tsx                      # Root component with router and providers
    ├── index.css / App.css          # Global styles
    │
    ├── layouts/
    │   └── DashboardLayout.tsx      # Shared sidebar + header shell for all dashboard pages
    │
    ├── contexts/
    │   └── SocketContext.tsx        # React context providing Socket.IO client to the component tree
    │
    ├── pages/
    │   ├── Index.tsx                # Landing / marketing page
    │   ├── NotFound.tsx             # 404 page
    │   └── dashboard/
    │       ├── Browse.tsx           # Browse jobs, skills, and materials marketplace
    │       ├── Calendar.tsx         # Calendar view for deadlines and milestones
    │       ├── Campus.tsx           # Campus Hub (discussions, polls, announcements)
    │       ├── Leaderboard.tsx      # Student contribution leaderboard
    │       ├── Messages.tsx         # Real-time direct and group messaging
    │       ├── MyWork.tsx           # Personal work dashboard (active projects, invoices)
    │       ├── Profile.tsx          # User profile and portfolio editor
    │       ├── Settings.tsx         # Account settings
    │       └── Wallet.tsx           # Wallet, transactions, escrow, savings goals
    │
    ├── components/
    │   ├── Header.tsx               # Top navigation bar
    │   ├── AuthModal.tsx            # Login / register modal
    │   ├── JobCard.tsx              # Job listing display card
    │   ├── JobPostCard.tsx          # Job posting form card
    │   ├── SkillCard.tsx            # Skill listing display card
    │   ├── SkillPostCard.tsx        # Skill posting form card
    │   ├── MaterialCard.tsx         # Material listing display card
    │   ├── MaterialPostCard.tsx     # Material posting form card
    │   ├── DatabaseConnectionTest.tsx
    │   ├── browse/                  # Browse page sub-components
    │   ├── campus/                  # Campus Hub sub-components
    │   ├── dashboard/               # Dashboard widget components
    │   ├── forms/                   # Reusable form components
    │   ├── messages/                # Chat UI components
    │   ├── modals/                  # Modal dialogs
    │   ├── mywork/                  # My Work section components
    │   ├── projects/                # Project management components
    │   ├── ui/                      # shadcn/ui primitives (auto-generated)
    │   └── wallet/                  # Wallet sub-components
    │
    ├── hooks/                       # Custom React hooks
    ├── services/                    # API service layer (Axios calls)
    ├── types/                       # Shared TypeScript type definitions
    └── lib/                         # Utility functions (e.g., cn() for class merging)
    │
    └── server/                      # Express backend (runs as a Node.js module)
        ├── index.js                 # Express app setup, Socket.IO, middleware, route registration
        ├── config/                  # Database connection pool configuration
        ├── middleware/
        │   └── authMiddleware.js    # JWT verification middleware
        ├── controllers/             # Route handler logic (one file per resource)
        ├── models/                  # Database query helpers / data access layer
        ├── routes/                  # Express Router definitions (one file per resource)
        │   ├── userRoutes.js
        │   ├── jobRoutes.js
        │   ├── applicationRoutes.js
        │   ├── skillRoutes.js
        │   ├── materialRoutes.js
        │   ├── contactRoutes.js
        │   ├── workRoutes.js
        │   ├── invoiceRoutes.js
        │   ├── notificationRoutes.js
        │   ├── walletRoutes.js
        │   ├── messageRoutes.js
        │   ├── projectRoutes.js
        │   ├── projectTaskRoutes.js
        │   ├── projectResourceRoutes.js
        │   ├── projectTimeRoutes.js
        │   ├── projectCommentRoutes.js
        │   └── campusRoutes.js
        └── database/
            ├── initDb.js                    # Auto-runs all schema files on startup
            ├── schema.sql                   # Core tables (users, jobs, skills, materials, etc.)
            ├── wallet_schema.sql            # Wallet, transactions, escrow tables
            ├── project_schema.sql           # Projects and milestones tables
            ├── project_enhanced_schema.sql  # Tasks, resources, time entries, comments, activity
            ├── campus_schema.sql            # Campus posts, comments, polls, likes, tags
            ├── message_schema.sql           # Direct and group messaging tables
            └── expense_categories_schema.sql
```

---

## ⚙️ Setup Instructions

### Prerequisites

- **Node.js** ≥ 18 (install via [nvm](https://github.com/nvm-sh/nvm#installing-and-updating))
- **npm** ≥ 9
- **MySQL** ≥ 8.0 running locally or accessible remotely

---

### 1. Clone the Repository

```sh
git clone https://github.com/pawpaw64/Earn-n-Learn-V1.git
cd Earn-n-Learn-V1
```

### 2. Install Dependencies

```sh
npm install
```

### 3. Configure Environment Variables

Create a `.env` file in the project root (copy from the example below and fill in your values):

```env
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=your_mysql_password
DB_NAME=dbEarn_learn
JWT_SECRET=your_super_secret_jwt_key
PORT=8080
```

### 4. Initialise the Database

The server auto-initialises the database and runs all schema migrations on first startup. Ensure your MySQL server is running and the credentials in `.env` are correct. The database `dbEarn_learn` will be created automatically if it does not exist.

If you prefer to run the schemas manually, execute each SQL file in order:

```sh
mysql -u root -p < src/server/database/schema.sql
mysql -u root -p < src/server/database/wallet_schema.sql
mysql -u root -p < src/server/database/project_schema.sql
mysql -u root -p < src/server/database/project_enhanced_schema.sql
mysql -u root -p < src/server/database/campus_schema.sql
mysql -u root -p < src/server/database/message_schema.sql
mysql -u root -p < src/server/database/expense_categories_schema.sql
```

### 5. Start the Application

```sh
node server.js
```

This single command:
- Initialises the database
- Starts the **Vite development server** (frontend) at `http://localhost:5173`
- Starts the **Express API server** (backend) at `http://localhost:8080`

> **Production build:** Run `npm run build` then `node src/server/index.js` to serve the compiled frontend as static files.

---

## 🔌 API Endpoints

All protected routes require a `Authorization: Bearer <token>` header obtained from the login endpoint.

Base URL: `http://localhost:8080/api`

### Authentication & Users — `/api/users`

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `POST` | `/register` | ❌ | Register a new user account |
| `POST` | `/login` | ❌ | Log in and receive a JWT token |
| `GET` | `/me` | ✅ | Get the currently authenticated user |
| `GET` | `/user/:id` | ✅ | Get a user profile by ID |
| `PUT` | `/profile` | ✅ | Update profile (with optional avatar upload) |
| `POST` | `/upload-avatar` | ✅ | Upload a profile avatar image |
| `POST` | `/skills` | ✅ | Add a skill to the user's profile |
| `DELETE` | `/skills/:skillId` | ✅ | Remove a skill from the user's profile |
| `POST` | `/portfolio` | ✅ | Add a portfolio item |
| `DELETE` | `/portfolio/:itemId` | ✅ | Remove a portfolio item |
| `POST` | `/websites` | ✅ | Add a website link |
| `DELETE` | `/websites/:websiteId` | ✅ | Remove a website link |

### Jobs — `/api/jobs`

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `GET` | `/` | ❌ | List all active job postings |
| `GET` | `/:id` | ❌ | Get a specific job by ID |
| `POST` | `/` | ✅ | Create a new job posting |
| `PUT` | `/:id` | ✅ | Update a job posting |
| `DELETE` | `/:id` | ✅ | Delete a job posting |
| `GET` | `/user/:userId` | ✅ | Get all jobs posted by a specific user |
| `GET` | `/:id/delete-permission` | ✅ | Check if the current user can delete a job |

### Applications — `/api/applications`

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `POST` | `/` | ✅ | Submit a job application (with optional resume upload) |
| `GET` | `/job/:jobId` | ✅ | List all applications for a job |
| `GET` | `/user` | ✅ | List all applications submitted by the current user |
| `PUT` | `/:id/status` | ✅ | Update application status (accept / reject) |

### Skills Marketplace — `/api/skills`

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `GET` | `/` | ❌ | List all skill listings |
| `GET` | `/:id` | ❌ | Get a skill listing by ID |
| `POST` | `/` | ✅ | Create a skill listing |
| `PUT` | `/:id` | ✅ | Update a skill listing |
| `DELETE` | `/:id` | ✅ | Delete a skill listing |
| `GET` | `/user/skills` | ✅ | Get skill listings by the authenticated user |

### Materials Marketplace — `/api/materials`

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `GET` | `/` | ❌ | List all material listings |
| `GET` | `/:id` | ❌ | Get a material listing by ID |
| `POST` | `/` | ✅ | Create a material listing (with image upload) |
| `PUT` | `/:id` | ✅ | Update a material listing |
| `DELETE` | `/:id` | ✅ | Delete a material listing |

### Contacts (Skill & Material Inquiries) — `/api/contacts`

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `POST` | `/skill` | ✅ | Send a contact request for a skill listing |
| `POST` | `/material` | ✅ | Send a contact request for a material listing |
| `GET` | `/skill/:skillId` | ✅ | Get all contacts for a skill listing |
| `GET` | `/material/:materialId` | ✅ | Get all contacts for a material listing |

### Projects — `/api/projects`

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `POST` | `/:applicationId/from-application` | ✅ | Create a project from an accepted application |
| `GET` | `/my-projects` | ✅ | List all projects for the authenticated user |
| `GET` | `/:id` | ✅ | Get project details including milestones |
| `PUT` | `/:id/status` | ✅ | Update project status |
| `PUT` | `/milestone/:milestoneId` | ✅ | Update a project milestone |
| `GET` | `/:id/activity` | ✅ | Get the project activity log |
| `POST` | `/:projectId/tasks` | ✅ | Create a task within a project |
| `PUT` | `/tasks/:taskId` | ✅ | Update a task |
| `DELETE` | `/tasks/:taskId` | ✅ | Delete a task |
| `POST` | `/:projectId/resources` | ✅ | Share a resource/file in a project |
| `DELETE` | `/resources/:resourceId` | ✅ | Remove a project resource |
| `POST` | `/:projectId/time` | ✅ | Log time against a project |
| `GET` | `/:projectId/time` | ✅ | Get time entries for a project |
| `PUT` | `/time/:entryId` | ✅ | Update a time entry |
| `POST` | `/:projectId/comments` | ✅ | Add a comment to a project |
| `GET` | `/:projectId/comments` | ✅ | Get all comments on a project |

### Wallet — `/api/wallet`

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `GET` | `/details` | ✅ | Get wallet balance and summary |
| `POST` | `/topup` | ✅ | Top up wallet balance |
| `POST` | `/withdraw` | ✅ | Withdraw funds from wallet |
| `GET` | `/transactions` | ✅ | List transaction history |
| `GET` | `/financial-data` | ✅ | Get income/expense chart data |
| `GET` | `/expense-breakdown` | ✅ | Get expense category breakdown |
| `GET` | `/payment-methods` | ✅ | List saved payment methods |
| `POST` | `/payment-methods` | ✅ | Add a payment method |
| `PUT` | `/payment-methods/:methodId/default` | ✅ | Set a default payment method |
| `DELETE` | `/payment-methods/:methodId` | ✅ | Remove a payment method |
| `GET` | `/savings-goals` | ✅ | List savings goals |
| `POST` | `/savings-goals` | ✅ | Create a savings goal |
| `PUT` | `/savings-goals/:goalId` | ✅ | Edit a savings goal |
| `PUT` | `/savings-goals/:goalId/add-funds` | ✅ | Add funds to a savings goal |
| `DELETE` | `/savings-goals/:goalId` | ✅ | Delete a savings goal |
| `GET` | `/escrow` | ✅ | List escrow transactions |
| `POST` | `/escrow` | ✅ | Create an escrow transaction |
| `POST` | `/escrow/:transactionId/release` | ✅ | Release escrow funds to provider |
| `POST` | `/escrow/:transactionId/dispute` | ✅ | Open a dispute on an escrow transaction |

### Messages — `/api/messages`

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `GET` | `/chats` | ✅ | List recent direct message conversations |
| `GET` | `/direct/:contactId` | ✅ | Get direct message history with a contact |
| `POST` | `/send` | ✅ | Send a direct message |
| `POST` | `/upload` | ✅ | Upload a file attachment for messaging |
| `GET` | `/users/search/:query` | ✅ | Search users to start a conversation |
| `POST` | `/groups` | ✅ | Create a group chat |
| `GET` | `/groups` | ✅ | List the user's group chats |
| `GET` | `/groups/find/:namePattern` | ✅ | Search for groups by name |
| `GET` | `/groups/:groupId/messages` | ✅ | Get group message history |
| `POST` | `/groups/message` | ✅ | Send a message to a group |
| `POST` | `/groups/members` | ✅ | Add a member to a group |
| `POST` | `/groups/:groupId/leave` | ✅ | Leave a group chat |
| `DELETE` | `/groups/:groupId/members/:userId` | ✅ | Remove a member from a group |
| `GET` | `/groups/:groupId/members` | ✅ | List members of a group |

### Campus Hub — `/api/campus`

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `POST` | `/posts` | ✅ | Create a post (question, discussion, announcement, poll) with optional attachment |
| `GET` | `/posts` | ✅ | List campus posts (filterable by type and tag) |
| `GET` | `/posts/search` | ✅ | Full-text search across campus posts |
| `GET` | `/posts/:id` | ✅ | Get a single post with details |
| `POST` | `/comments` | ✅ | Add a comment or reply to a post |
| `GET` | `/posts/:postId/comments` | ✅ | Get all comments on a post |
| `POST` | `/posts/:postId/like` | ✅ | Toggle like on a post |
| `POST` | `/comments/:commentId/like` | ✅ | Toggle like on a comment |
| `POST` | `/polls/:optionId/vote` | ✅ | Vote on a poll option |

### Notifications — `/api/notifications`

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `GET` | `/` | ✅ | List all notifications for the current user |
| `PUT` | `/:id/read` | ✅ | Mark a notification as read |
| `PUT` | `/read-all` | ✅ | Mark all notifications as read |

### Invoices — `/api/invoices`

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `GET` | `/` | ✅ | List invoices for the current user |
| `POST` | `/` | ✅ | Create a new invoice |
| `PUT` | `/:id` | ✅ | Update an invoice |
| `DELETE` | `/:id` | ✅ | Delete an invoice |

### Work — `/api/works`

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `GET` | `/` | ✅ | List all work items for the current user |
| `GET` | `/:id` | ✅ | Get a specific work item |

---

## 🗄 Database Schema

The database is named `dbEarn_learn` and is composed of several schema files that are applied in sequence on initialisation.

### Core Tables (`schema.sql`)

| Table | Description |
|---|---|
| `users` | Registered user accounts with profile fields (name, email, bio, university, course, graduation year, mobile) |
| `skills` | Profile skills linked to a user (not to be confused with skill marketplace listings) |
| `portfolio_items` | Portfolio projects/work samples linked to a user |
| `user_websites` | External links on a user's profile |
| `jobs` | Campus job/gig postings with type, payment, deadline, requirements, and status |
| `applications` | Job applications with cover letter, resume URL, and status tracking |
| `skill_marketplace` | Skill service listings with pricing, availability, and image |
| `material_marketplace` | Study material listings with price, condition, availability, and image |
| `skill_contacts` | Enquiries sent by students to skill listing owners |
| `material_contacts` | Enquiries sent by students to material listing owners |
| `invoices` | Invoices generated for completed work |
| `notifications` | In-app notifications linked to any resource type |

### Wallet Tables (`wallet_schema.sql`)

| Table | Description |
|---|---|
| `wallets` | One wallet per user storing the current balance |
| `payment_methods` | Saved card/payment method details (last4, expiry, provider) |
| `transactions` | Full ledger of all financial activity (deposits, withdrawals, payments, escrow movements) |
| `savings_goals` | Named savings targets with current and target amounts and deadline |
| `escrow_transactions` | Funds held in escrow between a client and a provider, linked to a job, skill, or material |

### Project Tables (`project_schema.sql`, `project_enhanced_schema.sql`)

| Table | Description |
|---|---|
| `projects` | Active engagements created from accepted applications, with status, timeline, and payment type |
| `project_milestones` | Phase-based milestones within a project |
| `project_updates` | Audit log of status changes and progress updates |
| `project_tasks` | Individual tasks within a project with priority, status, and assignment |
| `project_resources` | Files and links shared within a project |
| `project_time_entries` | Time logs submitted by project members |
| `project_comments` | Discussion thread attached to a project |
| `project_activity` | Comprehensive activity timeline for a project |

### Campus Hub Tables (`campus_schema.sql`)

| Table | Description |
|---|---|
| `campus_posts` | Posts of type question, discussion, announcement, or poll |
| `campus_poll_options` | Answer options for poll posts |
| `campus_poll_votes` | One vote per user per poll option |
| `campus_comments` | Nested comments on posts |
| `campus_tags` | Discoverable topic tags |
| `campus_post_likes` | Like associations between users and posts |
| `campus_comment_likes` | Like associations between users and comments |
| `campus_tag_followers` | Subscriptions to topic tags |

### Message Tables (`message_schema.sql`)

Contains tables for direct messages, group conversations, group memberships, and message read receipts.

---

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

1. **Fork** the repository and create a feature branch from `main`:
   ```sh
   git checkout -b feature/your-feature-name
   ```

2. **Commit** your changes with a clear, descriptive message:
   ```sh
   git commit -m "feat: add skill endorsement feature"
   ```

3. **Push** your branch and open a **Pull Request** against `main`. Describe what the PR changes and why.

4. Follow the existing code style:
   - TypeScript strict mode on the frontend
   - ES Modules (`import`/`export`) throughout
   - Controllers handle request/response logic; models handle database queries
   - All protected routes must use the `auth` middleware

5. Do **not** commit secrets, credentials, or the `.env` file.

---

## 📄 License & Acknowledgments

This project is licensed under the **ISC License**.

**Built with:**

- [React](https://reactjs.org/) — frontend UI
- [Vite](https://vitejs.dev/) — build tooling
- [shadcn/ui](https://ui.shadcn.com/) — component library
- [Tailwind CSS](https://tailwindcss.com/) — styling
- [Express.js](https://expressjs.com/) — backend framework
- [Socket.IO](https://socket.io/) — real-time communication
- [MySQL](https://www.mysql.com/) — database
- [TanStack Query](https://tanstack.com/query) — data fetching

