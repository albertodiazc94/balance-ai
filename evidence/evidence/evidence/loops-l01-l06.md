# Loops L01 and L06 — BalanceAI Session 14

## L01 — Improved PRD + Architecture Checklist

The weakest section of the current PRD is the acceptance criteria —
it is not always clear when a feature is done.

### Architecture checklist

- [x] Five layers defined: Frontend, Backend, Database, AI, Automation.
- [x] AI boundary documented — what AI can and cannot do.
- [x] Rule-based scheduling defined separately from AI.
- [x] Privacy and safety section documented.
- [ ] Auth not implemented yet.
- [ ] Supabase not connected yet.
- [ ] Error handling not defined.
- [ ] Environment variable management not in place.
- [ ] Deployment not configured.

### Weakest PRD section rewritten

Acceptance criteria added:
- A student can add 5 tasks and 3 fixed commitments and generate a weekly
  plan with no obvious conflicts.
- A busy day is flagged when work exceeds available time or recovery drops
  too low.
- The next best action mentions urgency, available time, energy, stress,
  and deadline proximity.
- The app suggests one free-time activity that fits available time, budget,
  city, and interest.
- The student can accept, edit, or dismiss every AI recommendation.

---

## L06 — Red-Team Log

| Objection | Severity | Response | Change made |
|---|---|---|---|
| Students won't trust an AI plan they didn't make themselves | High | Add plain-language explanations for every recommendation | Accept/edit/dismiss controls already in prototype |
| The AI may hallucinate time slots or override fixed commitments | High | Rule-based layer runs before AI — hard constraints are never touched by the model | Documented in ARCHITECTURE.md |
| Students may not complete onboarding if it takes too long | Medium | Onboarding target is under 3 minutes | Keep onboarding to max 5 fields |
| Privacy risk: stress and mood data is sensitive | High | All sensitive fields are optional | Documented in privacy section of ARCHITECTURE.md |
| Without real data the prototype cannot be properly tested | Medium | Use real tasks from a test student during the MVP experiment | Run experiment with one real user this week |
