# Architecture Overview

## Design Philosophy: Dumb Server, Smart LLM

SYMTHO's core architecture principle is that **all medical reasoning lives in the LLM prompt**, not in server code. The server is a stateless router that:

- Receives messages via WhatsApp webhook
- Manages session state (Redis, 24h TTL)
- Routes to the LLM with full conversation context
- Passes output through the safety engine
- Returns formatted response to the patient

This means we can update medical logic, add diseases, change triage thresholds — all without deploying new code. A prompt version update in the database changes system behavior instantly.

## Conversation Loop Architecture

The system runs a maximum of 3 conversation loops:

**Loop 1:** Patient provides initial symptoms → LLM analyzes and asks 1-2 follow-up questions

**Loop 2:** Patient responds → LLM has enough for preliminary triage OR asks one final question

**Loop 3 (forced final):** Regardless of information quality, LLM must output a final triage. The prompt explicitly states: "You have all available information. Provide your final assessment."

At every loop, the LLM outputs:
- Probable diagnosis
- ICD-11 code
- Triage color (green/yellow/red)
- Confidence score (0-100)

The conversation ends early if confidence reaches ≥90% before loop 3.

## Why 3 Loops Maximum?

In our field research, we found that rural Indian patients:
- Often have limited phone credit/data
- Are not accustomed to extended digital conversations
- Need a fast answer, not a thorough medical interview

3 loops balances diagnostic accuracy against user dropout. Our testing showed diminishing accuracy returns after loop 3.

## LLM Output Format

Every LLM call returns structured JSON:
```json
{
  "symptoms_identified": ["headache", "fever", "fatigue"],
  "next_question": "How many days have you had the fever?",
  "triage_color": "yellow",
  "confidence": 72,
  "reasoning": "Symptoms suggest viral infection but duration unknown"
}
```

This is validated against a schema before processing. Malformed responses trigger a retry (1x) then fallback to rule-based triage.
