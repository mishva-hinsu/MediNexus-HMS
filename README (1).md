# 🏥 MediNexus — Intelligent Hospital Management System

> A Django-based web application leveraging **Data Analytics** to simplify hospital appointment management, improve doctor-patient interaction, and deliver data-driven insights for smarter healthcare delivery.

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Django](https://img.shields.io/badge/Django-4.2_LTS-092E20)
![Chart.js](https://img.shields.io/badge/Chart.js-4.4-FF6384)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 📋 Table of Contents

- [About the Project](#-about-the-project)
- [Key Features](#-key-features)
- [Tech Stack](#-tech-stack)
- [System Architecture](#-system-architecture)
- [Installation & Setup](#-installation--setup)
- [Seed Database](#-seed-database)
- [Login Credentials](#-login-credentials)
- [Data Analytics Features](#-data-analytics-features)
- [Pages Overview](#-pages-overview)
- [Testing](#-testing)
- [Limitations](#-limitations)
- [Roadmap](#-roadmap)
- [Author](#-author)

---

## 📖 About the Project

**MediNexus** is an Intelligent Hospital Management System designed to digitize and streamline healthcare operations. The system serves three types of users — **Admins**, **Doctors**, and **Patients** — each with role-based dashboards and features.

What sets MediNexus apart is its **comprehensive Data Analytics Dashboard**, which turns raw operational data into real-time insight on hospital performance, appointment trends, doctor utilization, patient demographics, and blog engagement using interactive **Chart.js** visualizations.

Built during a Web Development internship at **Curio** (i-Hub, KCG Campus, Ahmedabad) as a final-year B.E. project for **Gujarat Technological University**.

---

## ✨ Key Features

### 🔐 Authentication & User Management
- Custom `AbstractUser` model with `is_doctor` / `is_patient` role flags
- Separate registration flows for Doctors and Patients
- Role-based access control enforced via `@doctor_required` / `@patient_required` decorators
- `DoctorProfile` and `PatientProfile` auto-created through Django signals
- Profile management with avatar upload and detailed medical info

### 📅 Smart Appointment System
- Book by selecting specialty → doctor → date → time slot
- **AJAX-powered doctor filtering** by specialty using the Fetch API (no page reload)
- 20 time slots across morning / afternoon / evening
- Priority levels: Low / Normal / High / Urgent
- Full lifecycle: Pending → Confirmed → Completed / Cancelled / No Show
- Doctor-side management interface with automatic notification triggers

### 💊 Digital Prescriptions
- Issued by doctors against completed appointments
- Medication list with dosage and frequency
- Special instructions and follow-up date tracking
- Patients access their complete medication history online

### 📁 Medical Records
- Five record types: Diagnosis, Lab Result, Imaging, Procedure, Clinical Note
- File attachment support
- Patient-accessible medical history

### 📝 Health Blog Platform
- Full CRUD with draft / publish workflow
- Auto-generated slugs, 8 categories, thumbnail uploads
- Nested comment system with author notifications
- View counter and reading-time estimates
- Category-based filtering and search

### ⭐ Doctor Rating & Review System
- Interactive 1–5 star UI with written reviews
- Unique constraint per patient-doctor pair
- Auto-aggregated ratings surfaced on doctor profiles

### 💳 Payment Module
- Razorpay-style checkout with **4 methods**: Card, UPI, Net Banking, Wallet
- Auto-generated invoice numbers (`MNX-YYYYMM-XXXXXX`)
- Lifecycle: pending → processing → completed → failed → refunded
- Appointment auto-confirmation on successful payment
- Printable invoices and one-click refunds with appointment cancellation

> ⚠️ **Note:** The payment gateway simulates the Razorpay flow locally. Live transactions require production API keys.

### 🔔 Smart Notifications
- 5 notification types: appointment, blog, system, rating, reminder
- Triggered automatically on key events
- Mark individual / all as read

### 📊 Data Analytics Dashboard (Core Feature)
- **9 interactive Chart.js visualizations**
- KPI cards with month-over-month growth tracking
- Top performing doctors ranking table
- **Patient History module** with a visual timeline and 4 dedicated charts

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|-----------|
| **Backend** | Python 3.10+, Django 4.2 LTS |
| **Frontend** | HTML5, CSS3 (custom design system), vanilla JavaScript |
| **Database** | SQLite (PostgreSQL-ready via Django ORM) |
| **Charts** | Chart.js 4.4 |
| **Icons** | Font Awesome 6.5 |
| **Fonts** | Google Fonts (Inter, Plus Jakarta Sans) |
| **Images** | Pillow |
| **Forms** | django-widget-tweaks |
| **UI Framework** | None — custom CSS with CSS Variables (no Bootstrap) |

**No CSS framework.** The interface is a custom design system: 1100+ lines with 50+ CSS Custom Properties, a five-level shadow hierarchy, and responsive breakpoints at 1024px, 768px, and 480px.

---

## 🏗 System Architecture

MediNexus follows Django's **MTV (Model-Template-View)** pattern across five apps:

```
MediNexus/
├── hospital/          # Django project settings & root URLs
├── users/             # Custom User model, auth, profiles, notifications
├── doctors/           # Blog CMS, categories, comments, doctor ratings
├── patients/          # Appointments, prescriptions, medical records
├── payments/          # Checkout, invoices, transaction & refund handling
├── analytics/         # Analytics dashboard, chart APIs, patient history
├── templates/         # All HTML templates
│   ├── base/          # Base layout, homepage
│   ├── users/         # Auth, profiles, doctor listings
│   ├── doctors/       # Doctor dashboard, blog templates
│   ├── patients/      # Patient dashboard, booking, records
│   ├── payments/      # Checkout, invoice, payment history
│   └── analytics/     # Dashboard & patient timeline
├── static/            # CSS, JS, images
├── seed/              # JSON fixture files
└── media/             # User uploads (not tracked in git)
```

**15 database models · 30+ URL endpoints · 26 templates**

| Layer | Technology | Responsibility |
|-------|-----------|----------------|
| Model | Django ORM + SQLite | Data models, relationships, business logic |
| Template | Django Templates + HTML5 + CSS3 | UI rendering, template inheritance |
| View | Django Views + Python | Request handling, aggregation, JSON serialization |
| Static | CSS3 + JavaScript + Chart.js | Styling, interactivity, visualization, AJAX |

---

## 🚀 Installation & Setup

### Prerequisites
- Python 3.10 or higher
- pip

### Step-by-Step Setup

```bash
# 1. Clone the repository
git clone https://github.com/mishva-hinsu/medinexus-hms.git
cd medinexus-hms

# 2. Create a virtual environment
python -m venv env

# 3. Activate it
# Windows:
env\Scripts\activate
# macOS / Linux:
source env/bin/activate

# 4. Install dependencies
pip install -r requirements.txt

# 5. Run database migrations
python manage.py makemigrations users doctors patients payments analytics
python manage.py migrate

# 6. Load base fixtures (specialties, categories, time slots)
python manage.py loaddata seed/specialties.json
python manage.py loaddata seed/categories.json
python manage.py loaddata seed/timeslots.json

# 7. Seed demo data (350+ interconnected records)
python manage.py seed_demo

# 8. Start the development server
python manage.py runserver
```

### Access the application

| | |
|---|---|
| Application | http://localhost:8000 |
| Analytics Dashboard | http://localhost:8000/analytics/ |
| Admin Panel | http://localhost:8000/admin/ |

> The repository ships without `db.sqlite3`. Steps 5–7 build the database from scratch, so you get a fully populated demo environment on first run.

---

## 🌱 Seed Database

The `seed_demo` management command generates **350+ interconnected records**:

| Data | Count |
|------|-------|
| Doctors | 10 (across all specialties) |
| Patients | 20 |
| Appointments | 150 (mixed statuses spanning 6 months) |
| Prescriptions | ~80 |
| Medical Records | ~40 |
| Blog Posts | 12 (with comments) |
| Doctor Ratings | ~80 |
| Time Slots | 20 |
| Specialties | 10 |
| Blog Categories | 8 |

---

## 🔑 Login Credentials

Demo accounts created by `seed_demo`:

| Role | Username | Password |
|------|----------|----------|
| **Admin** | admin | admin123 |
| **Doctor** | ananya | medinexus123 |
| **Doctor** | rajesh | medinexus123 |
| **Patient** | patient_amit | medinexus123 |
| **Patient** | patient_sunita | medinexus123 |

*All seeded doctors and patients use the password `medinexus123`.*

> ⚠️ These are local demo credentials for a development database only. Never deploy with them.

---

## 📊 Data Analytics Features

### Main Dashboard — 9 interactive Chart.js visualizations

| # | Chart | Type | Shows |
|---|-------|------|-------|
| 1 | Monthly Appointment Trend | Area | 12-month appointment volume |
| 2 | Appointment Status Distribution | Doughnut | Pending / Confirmed / Completed / Cancelled |
| 3 | Priority Distribution | Bar | Low / Normal / High / Urgent breakdown |
| 4 | Day-of-Week Analysis | Bar | Busiest appointment days |
| 5 | Daily Appointments | Line | Last 30 days, granular view |
| 6 | Rating Distribution | Horizontal Bar | 1–5 star review breakdown |
| 7 | Blog Category Distribution | Polar Area | Content category analysis |
| 8 | Patient Growth | Area | New patient registrations over time |
| 9 | Specialty Demand | Doughnut | Appointment volume per specialty |

### Patient History — 4 additional charts
Visit Frequency · Appointment Status · Doctors Visited · Specialties Consulted

Paired with a colour-coded visual timeline of every medical event (appointments, prescriptions, records) with filterable category tabs.

### KPI Metrics Tracked
- Total Doctors, Patients, Appointments
- Month-over-month appointment growth
- Completion rate & cancellation rate
- Platform average rating
- New patient registrations (30-day)
- Blog views & comment engagement
- Top performing doctors ranking

### Notable Implementation Details
- Complex Django ORM aggregations using `Count`, `Avg`, `Sum`, `F`, `Q`, `ExtractWeekDay`
- Custom `DecimalEncoder` for safe JSON serialization of Django `Decimal` fields
- Dedicated API endpoints for dynamic chart data updates

---

## 📸 Pages Overview

| Page | URL | Access |
|------|-----|--------|
| Home / Landing | `/` | Public |
| Login | `/users/login/` | Public |
| Register (Patient) | `/users/register/patient/` | Public |
| Register (Doctor) | `/users/register/doctor/` | Public |
| Doctor Listing | `/doctors/list/` | Public |
| Doctor Profile | `/doctors/profile/<id>/` | Public |
| Health Blog | `/doctors/blog/` | Public |
| Blog Detail | `/doctors/blog/<slug>/` | Public |
| Patient Dashboard | `/patients/dashboard/` | Patient |
| Book Appointment | `/patients/book/` | Patient |
| My Appointments | `/patients/appointments/` | Patient |
| My Prescriptions | `/patients/prescriptions/` | Patient |
| Medical Records | `/patients/medical-records/` | Patient |
| Payment Checkout | via **Pay** on a pending appointment | Patient |
| Payment History | user dropdown → Payment History | Patient |
| Doctor Dashboard | `/doctors/dashboard/` | Doctor |
| Manage Appointments | `/patients/manage/` | Doctor |
| Write Blog | `/doctors/blog/create/` | Doctor |
| My Blogs | `/doctors/blog/my-blogs/` | Doctor |
| Analytics Dashboard | `/analytics/` | Authenticated |
| Patient History | `/analytics/` → Patient History | Authenticated |
| Profile | `/users/profile/` | Authenticated |
| Notifications | `/users/notifications/` | Authenticated |
| Admin Panel | `/admin/` | Admin |

---

## 🧪 Testing

**21 manual black-box test cases**, all passing, across:

- **Functional** — registration, login, booking, prescriptions, blog CRUD, ratings
- **Integration** — appointments triggering notifications, ratings updating profiles
- **UI/UX** — responsive across desktop (1920px), tablet (768px), mobile (375px)
- **Chart rendering** — all 13 charts verified with populated and empty datasets
- **Role-based access** — doctor-only pages correctly denied to patients, and vice versa
- **Payments** — checkout, UPI/card processing, invoice generation, refund flow

---

## 🎨 Design Highlights

- **Custom design system** — CSS variables as design tokens for consistent theming
- **Colour system** — Primary `#0A6EBD` (medical blue), Accent `#12B886` (teal green), plus 5 semantic sets
- **Typography** — Inter for body, Plus Jakarta Sans for headings
- **Fully responsive** — CSS Grid + Flexbox, three breakpoints, mobile hamburger nav
- **Smooth animations** — Intersection Observer fade-ins, animated stat counters, auto-dismissing alerts
- **Accessibility-friendly** — semantic HTML5, proper contrast ratios

---

## ⚠️ Limitations

- **SQLite** — fine for development and small deployments; concurrent writes become a bottleneck at hospital scale
- **Simulated payments** — Razorpay flow is local-only; live capture needs production API keys
- **No real-time chat** between doctors and patients
- **In-app notifications only** — no email or SMS delivery yet
- **Single-hospital scope** — multi-hospital support needs architectural changes
- **No video consultation** / telemedicine

---

## 🗺 Roadmap

- [ ] PostgreSQL migration for production-grade concurrency
- [ ] Live Razorpay integration with webhook verification and settlement
- [ ] Email (SMTP) and SMS (Twilio) notification delivery
- [ ] WebRTC video consultations
- [ ] AI-powered symptom checker
- [ ] Predictive analytics for no-shows, peak hours, and resource planning
- [ ] Multi-language support (Hindi, Gujarati)
- [ ] React Native / Flutter mobile app on a Django REST API
- [ ] Lab information system integration
- [ ] Multi-hospital / clinic chain support

---

## 👤 Author

**Mishva Hinsu** — B.E. Computer Science & Engineering, New L.J. Institute of Engineering and Technology (GTU)

[LinkedIn](https://www.linkedin.com/in/mishva1201) · [GitHub](https://github.com/mishva-hinsu)

---

*Built with ❤️ using Django & Data Analytics*
*MediNexus — Intelligent Hospital Management System © 2026*
