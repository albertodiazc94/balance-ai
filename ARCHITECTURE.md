# BalanceAI Architecture

Status: finalized for the MVP prototype.

## 1. Architecture Overview

BalanceAI is a responsive web app for university students who need help turning scattered tasks, deadlines, fixed commitments, and wellbeing check-ins into a realistic weekly plan.

The architecture deliberately separates deterministic scheduling from AI-generated reasoning:

- Rules protect hard constraints such as fixed commitments, unavailable time, deadline proximity, recovery gaps, and conflict detection.
- The AI layer ranks options, explains trade-offs, adapts to feedback, and produces readable next-action recommendations.
- The frontend keeps the student in control through editable plan blocks, accept/edit/dismiss controls, and calm overload review.

This split is important because the MVP must feel helpful without allowing the AI to invent unsafe or unrealistic schedules.

## 2. Proposed Stack

- Frontend: responsive web app, built first as a static prototype and later as a React-style app.
- Backend/database: Supabase for users, preferences, tasks, commitments, check-ins, plans, plan blocks, recommendations, and activities.
- AI layer: OpenAI or Gemini API for recommendation explanations, task ranking language, overload explanations, and adaptive feedback.
- Scheduling logic: deterministic TypeScript rules before any LLM call.
- Prototype context: seeded mock activities, manual city input, and optional mock weather.
- Deployment target: static prototype first; later Netlify or similar for the class demo.

## 3. Main Screens

- Onboarding: collects priorities, preferred work hours, interests, city, and budget range in under three minutes.
- Home dashboard: shows week health, next best action, current check-in, next deadline, and week preview.
- Task inbox: lets users add, edit, complete, and prioritize tasks.
- Commitments: captures fixed events and unavailable time.
- Weekly plan: shows editable blocks for fixed commitments, academic work, personal tasks, recovery, and activities.
- Overload review: explains why a day is tight and offers specific fixes.
- Recommendations: stores next actions, wellbeing suggestions, edits, dismissals, and accepted recommendations.
- Settings/privacy: explains optional fields, stored preferences, and future consent controls.

## 4. Data Model

Suggested Supabase tables:

- `users`: id, email, display_name, created_at.
- `preferences`: user_id, preferred_work_hours, interests, goals, city, budget_range, recovery_target_minutes, privacy_flags.
- `tasks`: id, user_id, title, domain, deadline, estimated_minutes, importance, status, notes, created_at, updated_at.
- `commitments`: id, user_id, title, type, start_time, end_time, recurrence, location_label.
- `checkins`: id, user_id, stress_level, energy_level, mood_note, created_at.
- `plans`: id, user_id, week_start, status, generated_summary, created_at.
- `plan_blocks`: id, plan_id, source_type, source_id, title, start_time, end_time, block_type, editable_reason.
- `recommendations`: id, user_id, plan_id, type, recommendation_text, reason_text, status, source_context, created_at.
- `activities`: id, title, category, city, duration_minutes, budget_level, indoor_outdoor, energy_fit.

## 5. Planning Flow

1. The student completes onboarding.
2. The student adds tasks and fixed commitments.
3. The student completes a stress/energy check-in.
4. Rule-based scheduling identifies unavailable time, fixed-event conflicts, workload density, deadline pressure, and recovery gaps.
5. The AI receives structured context, not raw private history.
6. The AI returns a weekly plan summary, one next best action, and plain-language explanation.
7. The student accepts, edits, or dismisses the recommendation.
8. Feedback is stored so later recommendations avoid repeating rejected suggestions.

## 6. AI Behaviour Boundary

The AI can:

- Rank tasks by urgency, importance, deadline proximity, estimated duration, available time, stress, energy, and recovery.
- Explain why a plan block or recommendation fits the current week.
- Suggest one next best action.
- Suggest one wellbeing/free-time activity from mock data.
- Rephrase overload warnings in calm, specific language.
- Adapt recommendations after the user accepts, edits, or dismisses a suggestion.

The AI must not:

- Diagnose stress, anxiety, burnout, depression, or any mental health condition.
- Present wellbeing suggestions as medical advice.
- Book, pay, post, or change calendars without explicit approval.
- Override fixed commitments.
- Be the only protection against schedule conflicts.

## 7. Rule-Based Responsibilities

Rules handle:

- Fixed commitment conflicts.
- Deadline proximity.
- Available time windows.
- Maximum workload per day.
- Minimum recovery time.
- Duration feasibility.
- Overload scoring.
- Basic activity filtering by time, city, budget, and energy fit.

The rules layer runs before the LLM so that hard constraints remain testable and predictable.

## 8. Privacy And Safety

- Stress, mood, city, and budget are optional where possible.
- The MVP uses manual city input, not real-time location tracking.
- Sensitive check-in data is stored minimally.
- Wellbeing suggestions are framed as planning support, not therapy.
- Any future external action requires a confirmation step.
- User can edit or dismiss any AI-generated block.

## 9. Testing Plan

Unit tests:

- Task duration and deadline calculations.
- Fixed commitment conflict detection.
- Overload scoring from workload density, stress, energy, and recovery time.
- Activity filtering by time, budget, city, and energy fit.

Integration tests:

- Onboarding creates preferences.
- Task and commitment forms save correctly.
- Generate plan creates a plan with blocks and recommendations.
- Accept/edit/dismiss actions update recommendation status.

User acceptance tests:

- A student can add five tasks and three fixed commitments, then generate a weekly plan with no obvious conflicts.
- A busy day is flagged when work exceeds available time or recovery drops too low.
- The next best action mentions urgency, available time, energy/stress, and deadline proximity.
- The app suggests one free-time activity that fits available time, budget, city, and interest.

## 10. Deployment Path

MVP prototype:

- Static files: `landing.html`, `index.html`, `styles.css`, `app.js`, and `assets/balance-mark.svg`.
- Evidence screenshot: `evidence/balanceai-dashboard-evidence.png`.
- Upload package: project markdown files plus prototype files.

Later build:

- Move static prototype into a React or Lovable-generated app.
- Connect Supabase.
- Add backend rule functions.
- Add AI API call behind a server-side boundary.
- Deploy to Netlify or similar.
- Connect `balance-ai.me` through DNS in the later hosting session.

## 11. Current Known Limitations

- The current prototype is static and uses seeded data.
- Supabase is not connected yet.
- Google AI Studio and Stitch uploads require browser login.
- GitHub collaborator invitations require GitHub usernames or emails for each team member and the professor.
