# MindAid Assessments (Android XML + Kotlin)

A clean, **clinical-style assessment flow** built with **XML + Kotlin + ViewBinding** (no Jetpack Compose).  
Current implementation focuses on **RTCQ-TV (Treatment Version)**: a “Readiness to Change” questionnaire, answered on a **1–10 scale** with **auto-next** behavior.

This Android client is designed to **sync with a web control panel** (clinician dashboard) via API (Retrofit hooks included as stubs).

---

## ✅ What’s implemented right now

### App Flow
1. **Launch → Hi screen**
2. Tap **Start**
3. Answer **Question 1 → Question 12**
   - Answer using **1–10**
   - On tap: answer saves + **moves to next question instantly**
4. After Q12: **Summary screen**
   - Local save stub
   - Web sync stub queued

### Assessment
- **RTCQ-TV page 1 questions (1–12)** included (Bangla text).
- Input is always **1–10**.
- Internal scoring mapping implemented for RTCQ answers:
  - 1–2 → -2
  - 3–4 → -1
  - 5–6 → 0
  - 7–8 → +1
  - 9–10 → +2

---

## 🧱 Tech Stack (Android)
- Kotlin
- XML layouts
- ViewBinding
- Material Components
- ConstraintLayout
- Retrofit + Gson (for control panel sync – currently stubbed)
- OkHttp logging interceptor (ready to enable)

No Compose. No fragments needed yet (Activities only for clarity).

---

## 📁 Suggested Package Structure

# MindAid Assessments (Android XML + Kotlin)

A clean, **clinical-style assessment flow** built with **XML + Kotlin + ViewBinding** (no Jetpack Compose).  
Current implementation focuses on **RTCQ-TV (Treatment Version)**: a “Readiness to Change” questionnaire, answered on a **1–10 scale** with **auto-next** behavior.

This Android client is designed to **sync with a web control panel** (clinician dashboard) via API (Retrofit hooks included as stubs).

---

## ✅ What’s implemented right now

### App Flow
1. **Launch → Hi screen**
2. Tap **Start**
3. Answer **Question 1 → Question 12**
   - Answer using **1–10**
   - On tap: answer saves + **moves to next question instantly**
4. After Q12: **Summary screen**
   - Local save stub
   - Web sync stub queued

### Assessment
- **RTCQ-TV page 1 questions (1–12)** included (Bangla text).
- Input is always **1–10**.
- Internal scoring mapping implemented for RTCQ answers:
  - 1–2 → -2
  - 3–4 → -1
  - 5–6 → 0
  - 7–8 → +1
  - 9–10 → +2

---

## 🧱 Tech Stack (Android)
- Kotlin
- XML layouts
- ViewBinding
- Material Components
- ConstraintLayout
- Retrofit + Gson (for control panel sync – currently stubbed)
- OkHttp logging interceptor (ready to enable)

No Compose. No fragments needed yet (Activities only for clarity).

---

## 📁 Suggested Package Structure

# MindAid Assessments (Android XML + Kotlin)

A clean, **clinical-style assessment flow** built with **XML + Kotlin + ViewBinding** (no Jetpack Compose).  
Current implementation focuses on **RTCQ-TV (Treatment Version)**: a “Readiness to Change” questionnaire, answered on a **1–10 scale** with **auto-next** behavior.

This Android client is designed to **sync with a web control panel** (clinician dashboard) via API (Retrofit hooks included as stubs).

---

## ✅ What’s implemented right now

### App Flow
1. **Launch → Hi screen**
2. Tap **Start**
3. Answer **Question 1 → Question 12**
   - Answer using **1–10**
   - On tap: answer saves + **moves to next question instantly**
4. After Q12: **Summary screen**
   - Local save stub
   - Web sync stub queued

### Assessment
- **RTCQ-TV page 1 questions (1–12)** included (Bangla text).
- Input is always **1–10**.
- Internal scoring mapping implemented for RTCQ answers:
  - 1–2 → -2
  - 3–4 → -1
  - 5–6 → 0
  - 7–8 → +1
  - 9–10 → +2

---

## 🧱 Tech Stack (Android)
- Kotlin
- XML layouts
- ViewBinding
- Material Components
- ConstraintLayout
- Retrofit + Gson (for control panel sync – currently stubbed)
- OkHttp logging interceptor (ready to enable)

No Compose. No fragments needed yet (Activities only for clarity).

---

## 📁 Suggested Package Structure

com.yourmindaid.assessments
├─ model/
│ ├─ AssessmentAnswer.kt
│ ├─ AssessmentQuestion.kt
├─ repo/
│ ├─ AssessmentRepository.kt
├─ ui/
│ ├─ MainActivity.kt
│ ├─ AssessmentActivity.kt
│ ├─ SummaryActivity.kt
│ ├─ GridLayoutParamsUtil.kt
│ ├─ RtcqTvQuestions.kt
res/
├─ layout/
├─ values/
├─ drawable/


---

## 🧭 Screens (Activities)

### 1) MainActivity
**File:** `ui/MainActivity.kt`  
**Layout:** `res/layout/activity_main.xml`

- Shows a welcoming "Hi 👋"
- Explains the assessment format
- `Start` button routes to AssessmentActivity

### 2) AssessmentActivity
**File:** `ui/AssessmentActivity.kt`  
**Layout:** `res/layout/activity_assessment.xml`

- Shows question progress `Question X/12`
- Shows question text
- Renders a **1–10 scale** as buttons
- When user taps a number:
  - Answer is recorded
  - Auto-advances to next question
- Back and Skip supported

### 3) SummaryActivity
**File:** `ui/SummaryActivity.kt`  
**Layout:** `res/layout/activity_summary.xml`

- Confirms completion
- Shows answered count
- Indicates save + sync queued
- Restart button to redo assessment

---

## 🔧 Setup & Run

### Requirements
- Android Studio (latest stable)
- Android SDK 34 recommended
- Min SDK: 24

### Build
1. Open the project in Android Studio
2. Sync Gradle
3. Run `app` on emulator or real device

---

## 📦 Gradle Dependencies (important)

These are required to match the current code:

- Material Components
- ViewBinding enabled
- Retrofit (for future control panel sync)

---

## 🎨 UI / Theme

The UI is designed to feel:
- calm
- clinical
- non-judgmental
- readable in low-light (dark theme)

### Key resources
- `res/values/colors.xml`
- `res/values/themes.xml`
- `res/drawable/bg_gradient.xml`
- `res/drawable/card_gradient.xml`

---

## 🌐 Web Control Panel Sync (Planned)

The app is intended to send assessments to a clinician-controlled web panel.

Current state:
- `AssessmentRepository.syncToWebControlPanelAsync()` is a stub
- Retrofit is included in Gradle
- Next step is implementing:
  - DTOs
  - API interface
  - Auth token attach
  - POST submission endpoint
  - retry / offline queue (WorkManager)

Suggested endpoint shape (example):
- `POST /api/patient/assessments/submit`
- Body:
  - assessmentType
  - patientId/sessionId
  - answers (raw1to10 + mappedScore)
  - metadata (time, device, locale)

---

## 🧠 Clinical Notes (Safety + Interpretation)

This project is NOT intended to:
- diagnose users
- replace clinicians
- provide medical certainty

It is intended to:
- collect structured inputs
- support clinician workflows
- offer non-diagnostic summaries

Interpretations should be:
- careful
- respectful
- clearly labeled as screening

---

## 🗺️ Roadmap (Next Steps)

### Phase 1 (next)
- Add **Readiness Ruler screen** (importance/confidence/readiness)
- Compute RTCQ totals:
  - PC total
  - C total
  - A total
- Result screen with safe interpretation text

### Phase 2
- Add Login/Signup (role-based)
- Save data to Room (drafts + history)

### Phase 3
- Add remaining assessments:
  - PHQ-15, HADS, ASEX
  - SDS (substance selection + cutoff logic)
  - Y-BOCS Bangla
  - RDAS-B

### Phase 4
- Full control panel integration:
  - JWT auth
  - sync queue
  - conflict handling
  - clinician assignment & review

---

## 🧩 License / Ownership
This is a private project module intended to integrate into MindAid / YourMindAid ecosystem.

---
