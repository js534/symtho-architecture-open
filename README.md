# SYMTHO — AI Triage for Underserved Communities

SYMTHO is a WhatsApp-based AI healthcare triage system designed for rural India and LMIC markets. Patients describe symptoms via text or voice, and receive a triage recommendation (green/yellow/red) with guidance on next steps.

**No app download. No account. No payment. Just a WhatsApp message.**

## Why This Exists

- 3B+ people lack adequate healthcare access
- Rural India: 1 doctor per 11,000 patients
- Patients travel 100+ km to reach a clinic
- 60%+ of field interview respondents confirmed unmet need

## Architecture Principles

| Principle | Implementation |
|-----------|---------------|
| **Dumb server, smart LLM** | All medical logic lives in the LLM prompt. Server handles routing only. |
| **Privacy by design** | Zero PII stored. SHA-256 anonymization. Age bucketing. District-level location only. |
| **Safety-first** | 63+ rule deterministic safety engine overrides AI for life-threatening patterns. |
| **Accessibility** | WhatsApp as interface — works on any smartphone, 2G networks, no download. |

## Triage Flow

1. Patient sends symptoms via WhatsApp (text or voice)
2. AI conducts up to 3 conversation loops
3. Each loop: symptom analysis → follow-up question → confidence check
4. At ≥90% confidence OR loop 3: final triage output
5. Safety engine checks all outputs against 63+ red flag rules
6. Patient receives green/yellow/red recommendation

## Validation

- 635+ doctor-reviewed medical cases tested
- +90% diagnostic accuracy on text-based symptoms
- Zero hallucinated symptoms in production LLM testing
- Rule-based safety engine catches edge cases the AI misses

## Documentation

- [Architecture Overview](docs/architecture-overview.md)
- [Privacy by Design](docs/privacy-by-design.md)
- [Safety Engine (IMCEO)](docs/safety-engine.md)
- [Why WhatsApp?](docs/why-whatsapp.md)

## Status

🔨 MVP in active development (March 2026)

Built in Copenhagen. Starting with India.

## Contact

[symtho.com](https://symtho.com) · [LinkedIn](https://linkedin.com/company/symtho)
