<h1 align="center">Job Hunting Assistant</h1>

Job Hunting Assistant is a web application that helps IT professionals **organize and automate their job search**. It is built with **Laravel (PHP)** and focuses on:

- **Job aggregation** from multiple platforms.
- **CV & job matching** based on skills and keywords.
- **Application tracking** with statuses and follow-up reminders.
- **Skill gap analysis** and learning recommendations.

This README explains what the project does, how it is structured, and how to run it locally while you continue developing and pushing to GitHub.

---

## 1. Features & Modules

- **Job Aggregation Module**
  - Collects job listings from platforms like LinkedIn, Indeed, BrighterMonday, and company career pages (initially can be manual entry, then automated).
  - Filters jobs by role, location, and keywords.
  - Uses scheduled background jobs (cron + Laravel scheduler) to refresh listings.

- **CV & Job Matching Engine**
  - Allows users to upload their CV.
  - Extracts keywords/skills from the CV and compares them with job descriptions.
  - Produces a **match score** and lists missing or weak skills.

- **Application Tracking System (ATS)**
  - Users can record each application (company, role, source, date, status).
  - Tracks status changes (planned, applied, interview, offer, rejected, accepted).
  - Supports follow-up reminders and personal notes.

- **Skill Gap Analyzer**
  - Analyzes skills requested across many job posts.
  - Compares them against the user profile/CV.
  - Highlights missing/weak skills and suggests possible learning resources.

- **Notification & Alerts Module**
  - Sends alerts for new job matches.
  - Reminds users about follow-ups and interviews.
  - Uses email (and optionally messaging platforms) via Laravel's notification system.

---

## 2. Technology Stack

- **Backend:** PHP 8+ / Laravel 12
- **Frontend:** Blade templates, HTML, CSS, JavaScript
- **Database:** SQLite by default (can be switched to MySQL or PostgreSQL via `.env`)
- **Background Jobs:** Laravel scheduler + cron
- **Optional Scraping Services:** Python (Scrapy / BeautifulSoup) via HTTP APIs
- **Version Control:** Git + GitHub

---

## 3. Project Structure (High Level)

Key Laravel directories used in this project:

- `app/`
  - `Http/Controllers/` – controllers for job listings, applications, profiles, etc.
  - `Models/` – Eloquent models for `User`, `Job`, `Application`, etc.
- `database/migrations/` – database schema definitions.
- `resources/views/` – Blade templates for pages (dashboard, job list, application list).
- `routes/web.php` – web routes for UI pages.
- `routes/console.php` – scheduled commands for job aggregation and notifications.

As the project evolves, you will see modules corresponding to:

- **Job Aggregation** – commands + services to fetch and normalize jobs.
- **CV Matching** – services to parse CV text and compute match scores.
- **ATS** – controllers/views for managing applications.
- **Skill Gap Analysis** – services that analyze skills frequency.
- **Notifications** – mailables/notifications and scheduled jobs.

---

## 4. Getting Started (Local Development)

### 4.1 Prerequisites

- PHP 8.2+
- Composer
- Node.js + npm (for frontend assets)
- Git

### 4.2 Clone the Repository

```bash
git clone https://github.com/Sammymullern/Job-Hunting-Assistant.git
cd Job-Hunting-Assistant
```

### 4.3 Install PHP Dependencies

```bash
composer install
```

### 4.4 Environment Setup

Copy the example environment file and generate an app key:

```bash
cp .env.example .env
php artisan key:generate
```

By default, Laravel in this project will work with an **SQLite** database for quick local development. You can change this later to MySQL/PostgreSQL in `.env`.

If you want to keep SQLite:

- Ensure `database/database.sqlite` exists (Laravel's post-create script usually creates it).
- In `.env`, set:

```env
DB_CONNECTION=sqlite
DB_DATABASE=/absolute/path/to/your/project/database/database.sqlite
```

Then run migrations:

```bash
php artisan migrate
```

If you prefer MySQL/PostgreSQL, update the `DB_*` settings in `.env` and run migrations against that database.

### 4.5 Install Frontend Dependencies

```bash
npm install
npm run dev
```

### 4.6 Run the Application

```bash
php artisan serve
```

Visit `http://127.0.0.1:8000` in your browser. You should see the Laravel welcome page (which will later be replaced by the Job Hunting Assistant UI).

---

## 5. Development Workflow

- **Branching (optional but recommended):**
  - Work on feature branches like `feature/ats`, `feature/job-aggregation`.
- **Basic Git workflow:**
  - `git status` – check changes.
  - `git add .` – stage changes.
  - `git commit -m "Describe your change"` – commit.
  - `git push` – push to GitHub.

You already have the project connected to:

```text
origin  https://github.com/Sammymullern/Job-Hunting-Assistant.git
```

Any updates you make locally can be shared by committing and pushing.

---

## 6. Roadmap (Phases)

- **Phase 1 – Core Tracker & Manual Jobs**
  - User authentication (login/register).
  - Manual job entry.
  - Application tracking (status, notes, follow-ups).

- **Phase 2 – Automation & Matching**
  - Automated job aggregation (APIs or scraping services).
  - CV upload and parsing.
  - CV ↔ job keyword matching with scores.

- **Phase 3 – Insights & Alerts**
  - Skill gap analysis and recommendations.
  - Notification and alert system (email, optional messaging).
  - Dashboard with charts and metrics.

This README will evolve as these phases are implemented in the codebase.

---

## 7. License

This project is currently based on the Laravel framework, which is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).

