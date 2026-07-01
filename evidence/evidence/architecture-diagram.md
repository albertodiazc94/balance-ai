# BalanceAI Architecture Diagram

## Five Layers

| Layer | Description |
|-------|-------------|
| **Frontend** | index.html · styles.css · app.js — what the student sees and interacts with |
| **Backend** | TypeScript scheduling rules — hard constraints checked before any AI call |
| **Database** | Supabase — users, tasks, commitments, check-ins, plans, recommendations |
| **AI** | OpenAI / Gemini API — explanations, task ranking, recommendations, feedback adaptation |
| **Automation** | Plan regeneration triggered by check-in updates or task changes |

## Data Flow

Frontend → Backend → Database → AI → Automation

## Notes

- Rules layer runs before the LLM so hard constraints remain testable and predictable.
- AI is never the only protection against schedule conflicts.
- Automation is triggered by check-in updates or task changes, not on a fixed schedule.
