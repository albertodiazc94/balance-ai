# AI Startup Validation Board — BalanceAI Session 14

## The AI Hypothesis Stack

**Customer**
Busy university students aged 18-25, living away from home, with tasks and
deadlines scattered across multiple tools, who feel overwhelmed by planning.

**Problem**
Students spend significant time and mental energy trying to plan their week
manually, leading to last-minute stress, missed deadlines, and poor recovery time.

**Solution & UX**
An AI-generated weekly plan that adapts to stress, energy, and deadlines — and
explains every recommendation in plain language — is more trusted and useful
than manual planning.

**AI Technical**
The model can consistently produce conflict-free, realistic weekly plans with
clear explanations, without hallucinating time slots or overriding hard constraints.

## Riskiest Assumption (Leap of Faith)

Solution & UX hypothesis: if students do not trust or use the AI-generated plan,
the product has no value regardless of how well the technology works.

## MVP Experiment

**Hypothesis being tested:**
Students trust and use an AI-generated weekly plan more than their current
manual planning method.

**Test level:** Concierge (Wizard of Oz)

**Description:**
Show one real student the BalanceAI prototype (index.html). Let them interact
with it for 10-15 minutes using their own real tasks and deadlines.

**Method:**
Ask them to add 3-5 real tasks, do the stress/energy check-in, and generate
a weekly plan. Observe how they interact with the accept/edit/dismiss controls.

**Minimum success criterion:**
- The student accepts or edits at least 2 AI recommendations.
- The student rates the plan as more useful than their current method (4/5 or higher).

**Validated if:**
Student accepts at least 2 recommendations and says the plan feels realistic.

**Invalidated if:**
Student dismisses all recommendations or says the plan does not reflect
their real situation.

**Decision loop:**
- Validated → build further, connect Supabase.
- Invalidated → pivot the recommendation logic or UX.
