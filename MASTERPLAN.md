
# Student Stress Monitoring App 📊🧠

A Flutter-based mobile app (iOS & Android) plus web-dashboard for early detection of student stress via digital phenotyping, combining passive sensing, active check-ins, gamification, and an LLM-powered chatbot. Designed as part of a research study with exportable, anonymized data for analysis.

---

## Table of Contents

1. [Overview & Objectives](#overview--objectives)  
2. [Target Audience](#target-audience)  
3. [Core Features & Functionality](#core-features--functionality)  
   - [Passive Data Signals](#passive-data-signals)  
   - [Active Check-Ins & Surveys](#active-check-ins--surveys)  
   - [Gamification & Engagement](#gamification--engagement)  
   - [LLM-Powered Chatbot](#llm-powered-chatbot)  
   - [Admin Dashboard & Exports](#admin-dashboard--exports)  
4. [High-Level Technical Stack](#high-level-technical-stack)  
5. [Conceptual Data Model](#conceptual-data-model)  
6. [User Interface & Design System](#user-interface--design-system)  
   - [Style Guide](#style-guide)  
   - [Wireframe Appendix](#wireframe-appendix)  
7. [Security, Privacy & Ethics](#security-privacy--ethics)  
8. [Development Phases & Milestones](#development-phases--milestones)  
9. [Success Metrics & Analysis Plan](#success-metrics--analysis-plan)  
10. [Potential Challenges & Solutions](#potential-challenges--solutions)  
11. [Future Expansion Possibilities](#future-expansion-possibilities)  

---

## Overview & Objectives

- **Mission**: Detect early signs of stress in high-school and undergraduate students by analyzing passive phone signals and active self-reports.  
- **Research Goal**: Validate correlations between digital phenotypes and standardized stress measures (e.g., Perceived Stress Scale).  
- **Deliverables**:  
  1. Flutter mobile app with passive sensing & daily check-in  
  2. Web-based admin dashboard for data analytics & export  
  3. Research paper documenting methods, results, and recommendations  

---

## Target Audience

- **Primary Users**: High‐school and undergraduate students  
- **Study Cohorts**: Broadly available pilot group, with optional control arm (active surveys only)  
- **Admin Users**: Researchers and educators with dashboard access  

---

## Core Features & Functionality

### Passive Data Signals
- **Activity & Sleep**: accelerometer, gyroscope, screen on/off patterns  
- **Phone Usage**: app categories, session lengths, unlock frequency  
- **Location Rhythms**: time spent at home, campus, social venues  
- **Communications Metadata**: call/text counts (no content)

### Active Check-Ins & Surveys
- **Mandatory Daily Check-In**: 1–2 quick slider questions  
- **Weekly Deep-Dive Survey**: mood scales, sleep quality, contextual questions  
- **Baseline & Exit Surveys**: standardized stress inventory for ground truth  

### Gamification & Engagement
- **Streak Counter**: days-in-a-row check-ins  
- **Badges & Achievements**: e.g., 7-day streak, 30 check-ins  
- **Progress Meter**: “Well-being meter” fills as tasks complete  
- **Customizable Reminders**: one daily push notification, with quiet-hours settings  
- **Feedback Prompts**: thumbs-up/down on previous tips  

### LLM-Powered Chatbot
- **Integrated Check-In Flow**: conversation drives daily survey, captures typing & language signals  
- **On-Demand Coach**: friendly “well-being coach” tone with optional clinical mode  
- **Dedicated Chat Tab**: quick access to coping tips and mini-exercises  

### Admin Dashboard & Exports
- **Web App**: user management, cohort segmentation, anonymized data visualization  
- **Data Exports**: CSV/JSON of sensor logs, survey timestamps, chatbot transcripts  
- **Analysis Hooks**: integration points for Python/Jupyter pipelines  

---

## High-Level Technical Stack

| Layer                 | Recommendation                         | Why?                                                   |
| --------------------- | -------------------------------------- | ------------------------------------------------------ |
| Mobile App            | Flutter (Dart)                         | Single codebase for iOS & Android, strong plugin ecosystem |
| Backend & API         | Firebase (Auth, Firestore, Functions)  | Rapid prototyping, built-in analytics, secure rules    |
| Passive Sensing       | Platform-SDK plugins                   | Well-tested for sensor access, background services     |
| Chatbot & LLM         | OpenAI API + custom prompts            | State-of-the-art language understanding & analytics    |
| Web Dashboard         | React or Vue + Node.js backend         | Component-driven UI, easy data visualization (e.g., D3) |
| Data Storage          | Firestore + BigQuery export            | Real-time sync, scalable analytics storage             |

---

## Conceptual Data Model

```text
User {
  id: UUID
  profile: { name, age, level (HS/Undergrad), timezone }
  permissions: { sensorsEnabled[], notificationsEnabled }
}

PassiveSignal {
  userId: UUID
  timestamp: ISO8601
  type: Activity|Usage|Location|CommMeta
  payload: { … }
}

CheckIn {
  userId: UUID
  timestamp: ISO8601
  stressLevel: 0–100
  feedback: { thumbsUp?, note? }
}

Survey {
  userId: UUID
  timestamp: ISO8601
  instrument: Baseline|Weekly|Exit
  responses: { questionId: answer }
}

ChatInteraction {
  userId: UUID
  sessionId: UUID
  messages: [ { role: user|bot, text, timestamp } ]
  typingMetrics: { wpm, pauses }
}
````

---

## User Interface & Design System

### Style Guide

* **Color Palette**:

  * Primary: #4A90E2 (calm blue)
  * Secondary: #50E3C2 (soothing teal)
  * Accent: #F5A623 (warm orange)
  * Neutral: #F2F2F2, #333333
* **Typography**:

  * Headings: Inter Bold
  * Body: Inter Regular
* **Components**:

  * Cards: rounded corners, subtle shadow
  * Buttons: raised for primary actions, outlined for secondary
  * Heatmap cells: 5-level color gradient from green (low stress) to red (high stress)
* **Icons & Illustrations**:

  * Use simple line-icons for tips, badges, chatbot
  * Illustrations for onboarding steps

### Wireframe Appendix

*(See full ASCII wireframes at end of this document)*

1. **Home**: last check-in, heatmap, tips, suggestions, streak badge
2. **Check-In**: chat-driven slider + thumbs feedback
3. **Chat**: open text input, tip suggestions, mood prompts
4. **Onboarding**: consent form, permissions toggles, baseline survey link
5. **History**: calendar heatmap + list of past check-ins & feedback
6. **Settings**: notification schedule, data sharing toggles, export request

---

## Security, Privacy & Ethics

* **Informed Consent**: explicit form during onboarding, detailing data use & withdrawal
* **Data Anonymization**: strip personal identifiers in exports; use UUIDs
* **Encryption**: TLS in transit, AES-256 at rest
* **IRB Compliance**: document protocol, risk mitigation, and data retention policies
* **User Control**: granular toggles for each sensor; option to delete account & data

---

## Development Phases & Milestones

| Phase                  | Duration | Milestones                                    |
| ---------------------- | -------- | --------------------------------------------- |
| 1. Discovery & Design  | 2 wks    | Requirements, wireframes, style guide         |
| 2. Core App MVP        | 4 wks    | Passive sensing + daily check-in + heatmap    |
| 3. Gamification & Chat | 3 wks    | Streaks, badges, chatbot integration          |
| 4. Admin Dashboard     | 3 wks    | User management, data export, basic analytics |
| 5. Surveys & Research  | 2 wks    | Baseline & weekly surveys, control group      |
| 6. Pilot & Testing     | 4 wks    | Beta with test cohort, bug fixes, IRB review  |
| 7. Analysis & Publish  | 4–6 wks  | Data analysis, paper drafting, final tweaks   |

---

## Success Metrics & Analysis Plan

* **Engagement**: daily check-in rate, churn, feature usage
* **Predictive Accuracy**: correlation & RMSE vs. Perceived Stress Scale
* **Chatbot Metrics**: session length, completion rate, user satisfaction
* **Ethical Compliance**: % of users withdrawing, permission opt-outs

---

## Potential Challenges & Solutions

| Challenge                        | Mitigation                                      |
| -------------------------------- | ----------------------------------------------- |
| Battery drain from sensing       | Optimize sample rates, use OS-friendly APIs     |
| Low compliance or survey fatigue | Gamify, customize reminder times, limit prompts |
| Data privacy concerns            | Transparent consent, user-controlled toggles    |
| Platform sensor API differences  | Abstract via Flutter plugins + fallbacks        |

---

## Future Expansion Possibilities

* **Wearable Integration**: Fitbit, Apple Watch for heart rate & EDA
* **Peer Support**: optional moderated student forums
* **Predictive Alerts**: notify counselors if risk threshold crossed
* **Multi-Lang Support**: adapt for non-English speaking cohorts
* **Longitudinal Studies**: multi-year tracking & advanced ML models

---

# Appendix: ASCII Wireframes

<details>
<summary>1. Home</summary>

```
┌─────────────────────────────────────────┐
│ Good afternoon, [Name]                 │
│ Last Check-in: Moderate (Jun 6 @10:15) │
│ [🔥 5-day streak badge]                │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ Weekly Stress Heatmap                  │
│ Mon Tue Wed Thu Fri Sat Sun            │
│ ■   ▒   ░   ■   ■   ░   ░             │
└─────────────────────────────────────────┘

┌ Quick Tips →  ┌ Study Suggestions →    │
│ [💨 Relax]     │ [Pomodoro]            │
│ [🧘 Breathe]   │ [Time-Block]          │
│ …             │ …                     │
└─────────────────────────────────────────┘

[Nav: Home • Check-In • Chat • History • Settings]
```

</details>

<details>
<summary>2. Check-In (Chat Flow)</summary>

```
┌ Bot: “Hey [Name], how are you feeling?” ──┐
│ > [User types…]                          │
└──────────────────────────────────────────┘
┌ “On a scale of 0–100, your stress is?”   │
│ [────────|50|────────]                   │
│ [Submit]                                 │
└──────────────────────────────────────────┘
┌ “Did yesterday’s tips help?” 👍 👎       │
└──────────────────────────────────────────┘
```

</details>

<details>
<summary>3. Chat Tab</summary>

```
┌ Chat with Well-being Coach ──────────────┐
│ [… previous messages …]                  │
│ Bot: “Want a quick breathing exercise?”  │
│ > [User input…]                          │
└──────────────────────────────────────────┘
│ [ Text Input             ] [Send ▶︎]     │
```

</details>

<details>
<summary>4. Onboarding & Permissions</summary>

```
1. Welcome & Purpose  
2. Baseline Survey → Perceived Stress Scale  
3. Permissions: [Sensors] [Notifications]  
4. Data Sharing Controls  
5. Complete & Go to Home
```

</details>

<details>
<summary>5. History</summary>

```
┌ Weekly Heatmap (same as Home) ──────────┐
│                                         │
└─────────────────────────────────────────┘
┌ Past Check-Ins List                     │
│ • Jun 6 — Moderate — 👍                  │
│ • Jun 5 — High — 👎                      │
│ …                                       │
└─────────────────────────────────────────┘
```

</details>

<details>
<summary>6. Settings</summary>

```
• Notifications → daily time, quiet hours  
• Data Sharing → toggle each sensor  
• Export My Data → [Download CSV]  
• Delete Account & Data  
```

</details>
---