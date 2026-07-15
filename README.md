# 🏥 MediNexus — Intelligent Hospital Management System

> A Django-based web application leveraging **Data Analytics** to simplify hospital appointment management, improve doctor-patient interaction, and deliver data-driven insights for smarter healthcare delivery.

---

## 📋 Table of Contents

- [About the Project](#about-the-project)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [System Architecture](#system-architecture)
- [Installation & Setup](#installation--setup)
- [Seed Database](#seed-database)
- [Usage Guide](#usage-guide)
- [Login Credentials](#login-credentials)
- [Screenshots](#screenshots)
- [Data Analytics Features](#data-analytics-features)
- [Project Structure](#project-structure)

---

## 📖 About the Project

**MediNexus** is an Intelligent Hospital Management System designed to digitize and streamline healthcare operations. The system serves three types of users — **Admins**, **Doctors**, and **Patients** — each with role-based dashboards and features.

What sets MediNexus apart is its **comprehensive Data Analytics Dashboard** that provides real-time insights into hospital performance, appointment trends, doctor utilization, patient demographics, and blog engagement metrics using interactive **Chart.js** visualizations.

---

## ✨ Key Features

### 🔐 Authentication & User Management
- Separate registration for Doctors and Patients
- Role-based access control (Admin / Doctor / Patient)
- Profile management with avatars and detailed medical info
- Real-time notification system

### 📅 Smart Appointment System
- Patients book appointments by selecting specialty → doctor → date → time slot
- AJAX-powered dynamic doctor filtering by specialty
- Priority levels (Low / Normal / High / Urgent)
- Full lifecycle management: Pending → Confirmed → Completed / Cancelled
- Doctors can confirm, complete, or cancel appointments

### 💊 Digital Prescriptions
- Doctors issue prescriptions linked to completed appointments
- Medication details with dosage and frequency
- Special instructions and follow-up dates
- Patients access full prescription history

### 📁 Medical Records
- Doctors create medical records per appointment
- Record types: Diagnosis, Lab Result, Imaging, Procedure, Clinical Note
- File attachment support
- Patient-accessible medical history

### 📝 Health Blog Platform
- Doctors publish medical articles with categories
- Rich text content with thumbnails
- Draft / Published workflow
- Comment system with replies
- View counter and reading time estimates
- Category-based filtering and search

### ⭐ Doctor Rating & Review System
- Patients rate doctors (1-5 stars) with written reviews
- Aggregated ratings on doctor profiles
- Rating analytics in the dashboard

### 🔔 Smart Notifications
- Real-time notifications for appointment updates
- Blog comment alerts
- Rating notifications
- System announcements
- Mark individual / all as read

### 📊 Data Analytics Dashboard (Core Feature)
- **7 Interactive Charts** powered by Chart.js
- KPI cards with month-over-month growth tracking
- Comprehensive hospital-wide performance metrics
- Detailed breakdown tables and metric cards

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|-----------|
| **Backend** | Python 3.10+, Django 4.2 |
| **Frontend** | HTML5, CSS3 (Custom Design System), JavaScript |
| **Database** | SQLite (development) |
| **Charts** | Chart.js 4.4 |
| **Icons** | Font Awesome 6.5 |
| **Fonts** | Google Fonts (Inter, Plus Jakarta Sans) |
| **UI Framework** | Custom CSS with CSS Variables (no Bootstrap dependency) |

---

## 🏗 System Architecture

```
MediNexus/
├── hospital/          # Django project settings & URLs
├── users/             # Custom User model, Auth, Profiles, Notifications
├── doctors/           # Blog system, Categories, Ratings
├── patients/          # Appointments, Prescriptions, Medical Records
├── analytics/         # Data Analytics Dashboard & API
├── templates/         # All HTML templates
│   ├── base/          # Base layout, homepage
│   ├── users/         # Auth, profiles, doctor listings
│   ├── doctors/       # Doctor dashboard, appointment management
│   ├── patients/      # Patient dashboard, booking, records
│   ├── blog/          # Blog CRUD templates
│   └── analytics/     # Analytics dashboard
├── static/            # CSS, JS, images
├── seed/              # JSON fixture files
└── media/             # User uploads
```

---

## 🚀 Installation & Setup

### Prerequisites
- Python 3.10 or higher
- pip (Python package manager)

### Step-by-Step Setup

```bash
# 1. Clone or extract the project
cd MediNexus

# 2. Create virtual environment
python -m venv env

# 3. Activate virtual environment
# Windows:
env\Scripts\activate
# macOS/Linux:
source env/bin/activate

# 4. Install dependencies
pip install -r requirements.txt

# 5. Run database migrations
python manage.py makemigrations users doctors patients analytics
python manage.py migrate

# 6. Load seed data (specialties, categories, time slots)
python manage.py loaddata seed/specialties.json
python manage.py loaddata seed/categories.json
python manage.py loaddata seed/timeslots.json

# 7. Seed demo data (150 appointments, 10 doctors, 20 patients, blogs, etc.)
python manage.py seed_demo

# 8. Start the development server
python manage.py runserver
```

### Access the application
Open your browser and visit: **http://localhost:8000**

---

## 🌱 Seed Database

The `seed_demo` command creates realistic demo data:

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

| Role | Username | Password |
|------|----------|----------|
| **Admin** | admin | admin123 |
| **Doctor** | ananya | medinexus123 |
| **Doctor** | rajesh | medinexus123 |
| **Patient** | patient_amit | medinexus123 |
| **Patient** | patient_sunita | medinexus123 |

*All doctors and patients use password: `medinexus123`*

---

## 📊 Data Analytics Features

The Analytics Dashboard provides **7 interactive Chart.js visualizations**:

1. **Monthly Appointment Trend** (Area Chart) — 12-month appointment volume
2. **Appointment Status Distribution** (Doughnut Chart) — Pending/Confirmed/Completed/Cancelled
3. **Priority Distribution** (Bar Chart) — Low/Normal/High/Urgent breakdown
4. **Day-of-Week Analysis** (Bar Chart) — Busiest appointment days
5. **Daily Trend** (Line Chart) — Last 30 days granular view
6. **Rating Distribution** (Horizontal Bar) — 1-5 star review breakdown
7. **Blog Category Distribution** (Polar Area) — Content category analysis

### KPI Metrics Tracked:
- Total Doctors, Patients, Appointments
- Month-over-Month appointment growth
- Completion rate & Cancellation rate
- Platform average rating
- New patient registrations (30-day)
- Blog views & comment engagement
- Top performing doctors ranking

---

## 📂 Project Structure

```
4 Django Apps:
├── users       → Authentication, User models, Profiles, Notifications
├── doctors     → Blog CMS, Categories, Comments, Doctor Ratings
├── patients    → Appointments, Prescriptions, Medical Records, Time Slots
└── analytics   → Data Analytics Dashboard, Chart APIs

Custom Features:
├── Custom CSS Design System (no Bootstrap)
├── CSS Variables for theming
├── Responsive mobile-first layout
├── AJAX-powered specialty → doctor filtering
├── Chart.js interactive analytics
├── Role-based dashboards
└── Real-time notification system
```

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
| Doctor Dashboard | `/doctors/dashboard/` | Doctor |
| Manage Appointments | `/patients/manage/` | Doctor |
| Write Blog | `/doctors/blog/create/` | Doctor |
| My Blogs | `/doctors/blog/my-blogs/` | Doctor |
| Analytics Dashboard | `/analytics/` | Authenticated |
| Profile | `/users/profile/` | Authenticated |
| Notifications | `/users/notifications/` | Authenticated |
| Admin Panel | `/admin/` | Admin |

---

## 🎨 Design Highlights

- **Custom Design System** with CSS variables for consistent theming
- **Modern Medical UI** — clean, professional, healthcare-focused palette
- **Fully Responsive** — works on desktop, tablet, and mobile
- **Smooth Animations** — fade-in effects, hover transitions
- **Accessibility-friendly** — proper contrast ratios and semantic HTML

---

*Built with ❤️ using Django & Data Analytics*
*MediNexus — Intelligent Hospital Management System © 2026*
