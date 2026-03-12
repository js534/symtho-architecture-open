# IMCEO Safety Engine

## Why a Rule-Based Safety Layer?

LLMs are probabilistic. In healthcare, some patterns must ALWAYS trigger an emergency response regardless of what the AI thinks. The IMCEO engine is a deterministic safety net that runs AFTER every LLM output.

## How It Works

1. LLM returns triage color + identified symptoms
2. IMCEO checks symptoms against 63+ hardcoded red flag rules
3. If ANY rule matches → override triage to RED
4. Override is logged for audit
5. Patient receives emergency guidance

## Example Red Flag Rules

| Symptom Pattern | Override | Rationale |
|----------------|----------|-----------|
| Chest pain + shortness of breath | → RED | Possible MI / PE |
| Fever >5 days + rash (child <5) | → RED | Possible meningitis / dengue |
| Sudden severe headache + neck stiffness | → RED | Possible SAH |
| Pregnancy + vaginal bleeding | → RED | Possible ectopic / miscarriage |
| Loss of consciousness + seizures | → RED | Possible epileptic episode / poisoning |

## Design Decisions

**Why not put these rules in the LLM prompt?**

We do include red flags in the prompt as well. But prompt instructions can be inconsistent across edge cases. The IMCEO engine guarantees that critical patterns are never missed, regardless of LLM model version, prompt wording, or input quality.

**Why "IMCEO"?**

Internal Medical Chief Executive Officer — the engine acts as a final sign-off authority, like a chief medical officer reviewing every case before discharge.
