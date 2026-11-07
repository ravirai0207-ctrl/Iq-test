# 🧠 NeuroIQ — 3D Animated Cognitive IQ Testing Platform

An advanced, light-themed 3D animated web platform that conducts standardized psychometric IQ assessments with real-time Three.js graphics, email OTP verification, demographic calibration, and persistent backend storage (SQLite).

---

## ✨ Features

- **Luminous Light-Themed 3D Scene**:
  - Built with **Three.js** featuring a floating crystalline quantum core, faceted refractions, concentric orbital rings, and dynamic particle constellations.
  - Interactive mouse parallax tracking and responsive state transitions (breathing idle, OTP ripple, category-aware diagnostic rotation, high-speed neural scan, and celebratory bloom).
  - Clean light aesthetic with soft pearlescent gradients and modern frosted glassmorphic UI cards.

- **Email Verification via OTP**:
  - Secure 6-digit cryptographic OTP generation with a 10-minute validity countdown.
  - Supports **real live email dispatch** via standard SMTP (e.g., Gmail, Outlook, SendGrid) configured in `smtp_config.json`.
  - Includes an out-of-the-box **Dev Quick-Preview mode** with one-click auto-fill, allowing immediate local testing without needing SMTP credentials setup first.

- **Demographic & Psychometric Standardization**:
  - Calibrated by age groups (Youth, Young Adult, Fluid Peak, Calibrated Baseline, Mature Norms) using standardized psychometric norms (Gaussian Mean $\mu = 100$, Standard Deviation $\sigma = 15$).
  - 15 comprehensive questions spanning 5 core domains:
    1. **Visual Matrix Reasoning** (SVG transformation grids, rotational XOR superposition)
    2. **Numerical & Inductive Sequences** (Dual-interleaved series, polynomial differences)
    3. **3D Mental Geometry & Spatial Folding** (Unfolded cube nets, isometric projections)
    4. **Deductive Syllogisms & Set Theory**
    5. **Processing Velocity & Symbol Decoding**

- **Audio Synthesizer (Web Audio API)**:
  - Procedural sound generator: tactile glass clicks, harmonic chords, and celebratory chimes without external audio file dependencies. Mute toggle included in header.

- **Comprehensive Diagnostic Dashboard**:
  - Large radiant circular score badge with animated counter.
  - Interactive Gaussian population bell curve marking where the candidate ranks.
  - 5-Domain category breakdown with animated completion bars.
  - Official, high-resolution **Certificate of Cognitive Assessment** with Candidate Name, Verified Email, Age, Date, IQ Score, Percentile, and Verification ID, ready to print or save as PDF.

- **Live SQLite Backend Inspector & Leaderboard**:
  - Global Leaderboard showing top scores.
  - Built-in Database Inspector modal to view stored records in `users` and `test_results` tables live from the browser.

---

## 🚀 Quick Start

### 1. Launch the Server
From the project directory (`/Users/raviprakashrai/iq test`), run:
```bash
python3 server.py
```
The server will start listening at:
👉 **[http://localhost:8000](http://localhost:8000)**

### 2. Open in Browser
Open your browser and navigate to:
```
http://localhost:8000
```

---

## 📧 Configuring Real Email Dispatch (Optional)

By default, the server runs in **Dev Mode**, displaying the OTP verification code on screen for instant zero-config testing.

To send real emails to candidate inboxes, edit `smtp_config.json`:
```json
{
  "enabled": true,
  "smtp_host": "smtp.gmail.com",
  "smtp_port": 587,
  "smtp_user": "your-email@gmail.com",
  "smtp_pass": "your-app-password",
  "from_email": "noreply-iqtest@cognitivelabs.ai",
  "from_name": "CognitiveIQ Assessment Labs"
}
```
*(For Gmail, generate an App Password in your Google Account Security settings).*

---

## 🗄️ Database Architecture (`iq_test.db`)

The SQLite database persists all candidate data and submissions:

- **`users` Table**:
  - `id`: Auto-increment integer primary key
  - `name`: Candidate's full name
  - `age`: Candidate's age
  - `email`: Normalized email address (unique)
  - `otp_code`: 6-digit verification code
  - `otp_expires_at`: ISO timestamp for code expiration
  - `is_verified`: 1 for verified, 0 for pending
  - `session_token`: Active authenticated test session
  - `created_at`: Registration timestamp
  - `verified_at`: OTP confirmation timestamp

- **`test_results` Table**:
  - `id`: Primary key
  - `user_id`: Foreign key referencing `users.id`
  - `name`, `age`, `email`: Snapshot of demographic data
  - `iq_score`: Standardized psychometric IQ score
  - `percentile`: Global percentile rank
  - `classification`: Tier classification
  - `category_scores_json`: Detailed domain subscores
  - `answers_json`: Item-by-item response log
  - `time_taken_seconds`: Elapsed assessment time
  - `certificate_id`: Unique verifiable credential code
  - `completed_at`: Completion timestamp

