# 🏛️ FRA Risk Intelligence Platform

> **Enterprise Risk Intelligence & Supervisory Platform** for the Financial Regulatory Authority (FRA) to monitor, evaluate, and inspect Non-Banking Financial Institutions (NBFIs).

---

## 📋 Table of Contents
1. [Overview](#overview)
2. [Key Features & Capabilities](#key-features--capabilities)
3. [Technology Stack](#technology-stack)
4. [Repository Structure](#repository-structure)
5. [Getting Started & Installation](#getting-started--installation)
6. [Default Credentials](#default-credentials)
7. [Role-Based Access Control (RBAC)](#role-based-access-control-rbac)
8. [Risk Engine & Early Warning System (EWS)](#risk-engine--early-warning-system-ews)
9. [Security & Compliance](#security--compliance)
10. [License & Support](#license--support)

---

## Overview

The **FRA Risk Intelligence Platform** is a production-grade supervisory web dashboard engineered for financial regulators, auditors, and analysts. It automates financial risk scoring, early warning alert detection (EWS), risk-based field inspection scheduling, and task force management across non-banking financial sectors (Microfinance, Consumer Finance, Insurance, Capital Markets, Leasing, Real Estate Finance).

Built with **Python**, **Streamlit**, **SQLAlchemy**, and **Plotly**, the application features a high-density SaaS Admin interface with Western English digits (`0-9`), robust JWT authentication with strict session isolation, role-based access control (RBAC), SMTP automated email dispatch, and evidence report file management.

---

## Key Features & Capabilities

### 1. Fresh Session Isolation per Login
- **Isolated User Sessions**: On every login (manual form or quick demo buttons), previous session states and URL query parameters are purged (`st.session_state.clear()`) to eliminate cross-user state leakage or tab ghosting.
- **Unique JWT & Session Nonce**: Each login generates a fresh JWT token with a unique UUID `session_nonce` for tamper-proof authorization.

### 2. Role-Based Inspection Workflow & Inspector Portal
- **Dedicated Inspector Portal (`inspector` / `Inspector@123`)**: Shows exclusively the field inspection tasks assigned to the logged-in inspector (`assigned_to_user_id == user.id`).
- **Audit Findings & Evidence Upload**: Inspectors can log detailed violation notes, update task lifecycle statuses (`Scheduled`, `In Progress`, `Completed`, `Cancelled`), adjust evaluated entity risk levels, and upload audit evidence files (`.pdf`, `.docx`, `.xlsx`, `.png`, `.jpg`).
- **Manager Supervisory Review**: Admins & Risk Analysts review inspector submissions, add supervisory comments, approve/reject findings, and download attached evidence files.
- **Automated Email Dispatch (SMTP)**: Automatically sends email notifications to assigned inspectors upon task dispatch and to managers upon field findings submission.

### 3. Executive Oversight & Interactive Dashboards
- **Strategic KPIs**: Real-time stats on total monitored entities, risk level distributions (High, Medium, Low), aggregate loan portfolios, and complaints resolution rates.
- **Interactive Visualizations (Plotly)**: Risk heatmaps by sector, complaint category breakdowns, and historical risk score trends.
- **Live Alerts Feed**: High-visibility ticker highlighting entities crossing critical risk thresholds.

### 4. Company Deep-Dive & Financial Analytics
- **Comprehensive Entity Profiles**: Deep analytics covering financial stability, executive governance, supervisory ratings, and complaint volumes.
- **Statutory Audit File Downloads**: Attached regulatory reports and evidence files are downloadable directly from modal popups and deep-dive views.

### 5. Dynamic & Configurable Risk Engine
- **Adjustable Weight Matrix**: Risk Analysts can dynamically tweak weights for financial ratios, complaint frequency, and regulatory violations with real-time score recalculation.
- **Composite Risk Scoring**: Merges financial performance scores with operational complaints to produce an overall risk score from 0 to 100.

### 6. Admin Control Panel & Governance
- **Full Entity Deletion (Cascade Purge)**: Dedicated subtab for purging monitored entities alongside all associated records (financials, complaints, inspection tasks, risk histories, and reports).
- **User Account Management**: Admins can register new users, update user roles, toggle account active status, or permanently delete accounts.
- **Security Audit Logging**: Full system activity logging tracking user actions, timestamps, and IP addresses.

### 7. Western Numerals & Official FRA Branding
- **Strict Western English Digits (`0-9`)**: Global CSS typography rules enforce Western numerals across all metrics, tables, forms, and dialogs.
- **Official Palette**: Navy Blue (`#0F172A`), Regal Gold (`#D97706`), and Slate styling with light/dark theme toggles.

---

## Technology Stack

| Component | Technology Used |
| :--- | :--- |
| **Language** | Python 3.10+ |
| **Frontend Framework** | [Streamlit](https://streamlit.io/) with Custom Enterprise CSS |
| **Database & ORM** | SQLAlchemy (Supports **MySQL / MariaDB** via XAMPP with fallback to **SQLite**) |
| **Data & Analytics** | Pandas, NumPy, Plotly Express & Graph Objects |
| **Security & Auth** | PyJWT, Passlib (Bcrypt hashing), Bleach (HTML input sanitization) |
| **Email Service** | Python `smtplib` / `email.mime` |

---

## Repository Structure

```
fra/
├── app.py                      # Main entry point & role-based view routing
├── auth.py                     # JWT token encoding/decoding & bcrypt password hashing
├── config.py                   # Environment, security keys & database URL configurations
├── database.py                 # SQLAlchemy engine & session creation
├── models.py                   # ORM Database models & schema definitions
├── setup_db.py                 # Automated SQL database creation & data seeding script
├── custom_theme.py             # Enterprise SaaS light/dark CSS design system
├── requirements.txt            # Python dependencies
├── README.md                   # Full project documentation
│
├── risk_engine/                # Risk calculation algorithms & scoring rules
│   ├── financial.py            # Financial ratio risk algorithms
│   └── complaints.py           # Complaint severity risk scoring
│
├── utils/                      # Helper utilities
│   ├── security.py             # Input sanitization & audit log recording
│   ├── notifications.py        # Live notification center helper
│   ├── company_manager.py      # Entity management & cascade deletion handler
│   ├── company_modal.py        # Comprehensive entity popup dialog modal
│   └── data_seeder.py          # Synthetic dataset generator
│
└── views/                      # UI Views & Dashboards
    ├── login.py                # Supervisory access login with session isolation
    ├── executive_dashboard.py  # Executive oversight & KPI dashboard
    ├── company_deepdive.py     # Entity risk deep-dive & report generator
    ├── analyst_hub.py          # Risk Analyst hub & weight adjustments
    ├── inspection_scheduler.py # Risk-based inspection scheduler & inspector portal
    └── admin_panel.py          # Admin control panel, user management & audit logs
```

---

## Getting Started & Installation

### Prerequisites
- **Python 3.10** or higher
- Git
- (Optional) XAMPP / MySQL Server

### Step-by-Step Installation

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/belalmostafa966-ops/fra-risk-platform.git
   cd fra-risk-platform
   ```

2. **Create & Activate Virtual Environment:**
   ```bash
   # Windows
   python -m venv venv
   .\venv\Scripts\activate

   # Linux / macOS
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Initialize Database & Seed Records:**
   Run the database setup script to build tables and insert seed data:
   ```bash
   python setup_db.py
   ```

5. **Launch the Web Application:**
   ```bash
   streamlit run app.py
   ```
   Open your browser and navigate to: **`http://localhost:8501`**

---

## Default Credentials

Use these pre-configured accounts for testing different user roles:

| Username | Email | Password | Role | Access Level |
| :--- | :--- | :--- | :--- | :--- |
| `admin` | `admin@fra.gov.eg` | `Admin@123` | **Admin** | Full system access, User Management, Cascade Entity Deletion, Audit Logs |
| `analyst` | `analyst@fra.gov.eg` | `Analyst@123` | **Risk Analyst** | Risk Weights Configuration, Inspection Dispatch & Manager Review, Financial Analytics |
| `executive` | `executive@fra.gov.eg` | `Exec@123` | **Executive** | Strategic Executive Dashboard & Company Deep-Dive Analytics |
| `inspector` | `inspector@fra.gov.eg` | `Inspector@123` | **Inspector** | Dedicated Inspection Portal, Findings Logging, Evidence File Upload |

---

## Role-Based Access Control (RBAC)

1. **Administrator (`admin`):**
   - User account lifecycle management (Create, Update Role, Toggle Active, Delete).
   - Cascade entity deletion with database cleanup.
   - Access to full security audit logs.

2. **Risk Analyst (`analyst`):**
   - Configure dynamic risk engine weights.
   - Dispatch inspection tasks to field inspectors.
   - Review and approve/reject inspector audit findings.

3. **Field Inspector (`inspector`):**
   - Access restricted to assigned inspection tasks.
   - Record field audit notes and adjust assessed entity risk levels.
   - Upload evidence documents (`.pdf`, `.docx`, `.xlsx`, `.png`, `.jpg`).

4. **Executive (`executive`):**
   - Strategic high-level overview of NBFI sector risks.
   - Real-time early warning system (EWS) monitoring.

---

## Risk Engine & Early Warning System (EWS)

The platform evaluates risk through a weighted composite formula:

$$\text{Composite Risk Score} = (w_f \times \text{Financial Risk}) + (w_c \times \text{Complaints Risk}) + (w_v \times \text{Violations Risk})$$

- **Core Financial Ratios Assessed:**
  - Capital Adequacy Ratio (CAR)
  - Non-Performing Loans Ratio (NPL Ratio)
  - Return on Assets (ROA)
  - Liquidity Ratio
- **Risk Tiers:**
  - 🟢 **Low Risk:** 0 – 33
  - 🟡 **Medium Risk:** 34 – 66
  - 🔴 **High Risk:** 67 – 100 (Triggers priority field inspection dispatch)

---

## Security & Compliance

- **Input Sanitization**: All form inputs are sanitized using `bleach` to block XSS attacks.
- **Session Privacy**: Strict session cleanup prevents session bleed across different logins or open browser tabs.
- **Audit Logging**: Comprehensive logging records all system events with timestamps and user identifiers.

---

## License & Support

This project is built for supervisory and educational demonstration for the **Financial Regulatory Authority (FRA)**.  
All Rights Reserved © 2026.
