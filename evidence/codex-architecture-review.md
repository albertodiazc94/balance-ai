# Codex Architecture Review — BalanceAI Session 14

## Question 1: Is the architecture sound for an MVP at this stage?

Yes, the architecture is sound for an MVP prototype at this stage, with one important caveat: it is conceptually strong, but not yet technically complete enough to be a real deployable MVP.

The strongest architectural choice is the separation between deterministic scheduling rules and the AI layer. Hard constraints like deadlines, fixed commitments, unavailable time, recovery gaps, and conflicts should not depend on an LLM. Using AI mainly for ranking, explanations, trade-offs, and feedback adaptation is a good MVP decision because it reduces hallucination risk and keeps the student in control.

However, before this becomes a usable MVP, the architecture needs a few missing foundations:
- Auth is not implemented yet.
- Supabase is not connected yet.
- Environment variables and API key handling are missing.
- Deployment is not configured.
- The automation layer is described, but not technically implemented yet.
- AI failure handling should be defined.

Conclusion: BalanceAI has a sound MVP architecture direction. It is suitable for a static prototype and product validation, but the next technical step is to connect Supabase, add auth, protect AI API calls, configure deployment, and implement basic error handling.

## Question 2: What is structurally missing?

BalanceAI is structurally missing:
- Auth and user sessions
- A real Supabase data layer
- Error handling and fallback behavior
- Secure environment variable management
- Deployability (Netlify or similar)

The architecture is still valid for an MVP, but right now it is closer to a static prototype than a functional product.

## Question 3: Top 5 technical tasks before Deliverable 2

1. Implement Supabase Auth and user sessions.
2. Build the core Supabase data layer.
3. Move AI calls behind a secure backend or serverless function.
4. Implement scheduling error handling and overload states.
5. Configure deployment and environment management.

## Question 4: Biggest risks if we ship as-is

1. User data is not persistent, so students cannot trust the plan.
2. Auth is missing, creating privacy and data access risks.
3. AI recommendations may be misleading without validation or fallback.
4. The app may fail silently because error handling is not defined.
5. The product cannot be tested properly without deployment and environment setup.

Conclusion: BalanceAI is fine as a static validation prototype, but it should not be treated as a real MVP until auth, Supabase persistence, secure AI calls, error handling, and deployment are added.
