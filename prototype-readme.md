# AI Tutor — Spec Final (Day 6)

---

# 1. AI Product Canvas

## Value

Students often get stuck when learning complex concepts (e.g. machine learning, programming) and do not have immediate support.

The AI Tutor provides step-by-step explanations instead of giving direct answers, helping students:

* Understand concepts deeply
* Reduce frustration
* Learn independently

## Trust

To ensure users trust the system:

* The AI avoids giving final answers directly
* Provides step-by-step reasoning
* Uses simple explanations tailored to student level
* Encourages follow-up questions

Additionally:

* Displays uncertainty when needed
* Encourages verification instead of blind trust

## Feasibility

This product is feasible with current technology:

* LLM APIs (e.g. GPT-4o-mini)
* Simple web-based UI (HTML/CSS/JS)
* No need for complex infrastructure

Cost is low and suitable for rapid prototyping in a hackathon setting.

## Learning Signals (CRITICAL)

We track whether learning actually happens:

* Follow-up rate (% of users asking clarification questions)
* Completion rate (% users who say they understand after explanation)
* Correction rate (% of responses corrected by users)

These signals reflect real learning behavior instead of just engagement.

---

# 2. User Stories — 4 Paths

## 1. Happy Path

* User asks a question
* AI provides step-by-step explanation
* User understands concept
* User proceeds with learning

## 2. Low-Confidence Path

* AI gives explanation
* User is unsure
* User asks follow-up question
* AI refines explanation

This is expected and desirable — indicates engagement.

## 3. Failure Path

* User asks complex or ambiguous question
* AI gives incorrect or misleading explanation
* User may misunderstand concept

Risk: learning incorrect knowledge

## 4. Correction Path

* User identifies issue in explanation
* User challenges AI
* AI revises answer or clarifies uncertainty

This path is critical for trust and learning accuracy.

---

# 3. Evaluation Metrics

We define 3 core metrics:

## 1. Helpfulness Score

* Measured via user feedback (1–5)
* Target: > 4.0

Why: Measures perceived learning value

## 2. Follow-up Rate

* % of sessions with at least 1 follow-up question
* Target: > 40%

Why: Indicates engagement and deeper thinking

## 3. Correction Rate

* % of responses flagged or corrected by users
* Target: < 20%

Why: High correction rate indicates hallucination or poor explanations

---

## Precision vs Recall Decision

* We prioritize RECALL in explanations
  → Better to provide more context than miss key concepts

* But maintain PRECISION in factual correctness
  → Avoid hallucinations in core knowledge

This balance ensures both depth and accuracy.

---

## Red Flags

* Helpfulness < 3.5
* Correction rate > 30%
* Users stop asking follow-up questions

These indicate product failure.

---

# 4. Top 3 Failure Modes

## 1. Hallucination

* Trigger: Complex or niche questions
* Consequence: Students learn incorrect information

Mitigation:

* Force step-by-step reasoning
* Add uncertainty phrases
* Encourage verification

---

## 2. Overconfidence

* Trigger: Model gives confident tone even when unsure
* Consequence: Users blindly trust wrong answers

Mitigation:

* Explicit uncertainty handling
* Add phrases like “This may depend on context”

---

## 3. Too Generic Explanation

* Trigger: Vague or overly broad answers
* Consequence: Users still confused

Mitigation:

* Ask clarifying follow-up questions
* Personalize explanations

---

# 5. ROI — 3 Scenarios

## Conservative

* Users: 100
* Use case: small classroom testing
* Value: validate learning behavior

## Realistic

* Users: 1,000
* Use case: multiple classes
* Value: measurable improvement in learning engagement

## Optimistic

* Users: 10,000+
* Use case: university-wide adoption
* Value: scalable AI tutoring system

---

## Assumptions

* Students are willing to use AI for learning
* AI explanations are helpful enough
* Cost per query remains low

---

## Kill Criteria (IMPORTANT)

We stop development if:

* Helpfulness score < 3.5
* Correction rate > 30%
* No measurable improvement in engagement

---

# 6. Mini AI Spec

## Input

* User question (text)

## Output

* Step-by-step explanation
* Optional clarification question

## Model

* GPT-4o-mini (cost-efficient, fast)

## Prompt Design

System prompt:

* Act as a tutor
* Do NOT give direct answers
* Explain step-by-step
* Encourage thinking

## Example Prompt Behavior

User: “What is gradient descent?”

AI:

* Explain concept simply
* Give intuitive analogy
* Break into steps
* Ask follow-up question

---

## Success Criteria

* User understands concept
* User asks follow-up questions
* User corrects AI when needed

---

# FINAL NOTE

This product is designed as AUGMENTATION, not AUTOMATION.

The goal is not to replace learning, but to guide it.
