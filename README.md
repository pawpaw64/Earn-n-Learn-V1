# Earn-n-Learn

> A full-stack campus productivity platform that empowers students to earn income, share skills, trade materials, collaborate on projects, and connect with peers — all within one unified ecosystem.
>
---
**Project:** Earn-N-Learn 

**Institution:** United International University — Department of CSE 

**Course:** CSE 3412 — Database Managment System

**Group:** Team LongBLOB 

**Authors:** Tabassum Sumaiya · Md. Hasibul Hossain · Moumita Borna 



This repository contains the development resources for the EarnNLearn project 

## 🎥 Demo Video

[![Watch the demo](https://img.youtube.com/vi/jBf_TcsDPIE/0.jpg)](https://youtu.be/jBf_TcsDPIE)

---

## Table of Contents

1. [Project Overview](#-project-overview)
2. [Key Features](#-key-features)
3. [Technology Stack](#-technology-stack)
4. [Setup Instructions](#-setup-instructions)
5. [Database Schema](#-database-schema)
6. [Contributing](#-contributing)
7. [License & Acknowledgments](#-license--acknowledgments)

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
| **Tailwind CSS** | Utility-first CSS framework for rapid, consistent styling |
| **shadcn/ui + Radix UI** | Accessible, unstyled component primitives with ready-to-use shadcn wrappers |
| **Socket.IO Client** | Real-time bidirectional communication for the messaging system |
| **Axios** | HTTP client for all REST API calls |
| **Lucide React** | Icon set consistent with the shadcn design system |


### Backend

| Technology | Purpose |
|---|---|
| **Node.js** | JavaScript runtime for the server |
| **Express.js** | Minimal web framework providing REST API routing and middleware |
| **Socket.IO** | WebSocket-based real-time messaging (direct and group chats) |
| **MySQL 2** | Relational database driver with promise support |
| **bcryptjs** | Password hashing for secure credential storage |
| **JSON Web Tokens (JWT)** | Stateless authentication via bearer tokens |
| **CORS** | Cross-origin resource sharing configuration |

### Database

| Technology | Purpose |
|---|---|
| **MySQL** | Primary relational database. Chosen for structured relationships between users, jobs, projects, wallets, and marketplace listings |

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

