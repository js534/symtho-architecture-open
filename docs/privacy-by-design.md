# Privacy by Design

## Core Principle

Phone numbers are NEVER stored in plaintext. The entire system is designed so re-identification is impossible.

## Anonymization Pipeline

| Layer | Method | Detail |
|-------|--------|--------|
| Phone number | SHA-256 hash | `anon_hash = SHA-256(phone + salt)`. Salt rotates monthly. Original deleted from memory immediately. |
| Age | Bucketing | Exact age never stored. Buckets: 0-4, 5-14, 15-24, 25-34, 35-44, 45-54, 55-64, 65+ |
| Location | Generalization | Full PIN code never stored. Only first 3 digits (district level). 302001 → 302xxx |
| Free text | PII scrubbing | All free-text fields pass through PII detector before database write |
| Images | Perceptual hash only | Original images deleted after AI analysis. Only 64-bit pHash fingerprint stored |

## What We Store

- Anonymized hash (not reversible to phone number)
- Age bucket (not exact age)
- Gender
- District-level location (not address)
- Structured symptom data
- Triage result
- AI confidence score

## What We Never Store

- Phone numbers
- Names
- Addresses
- Original images
- Any data that could identify an individual

## Data Retention

- Session data: 24 hours (Redis TTL), then auto-deleted
- Triage records: Append-only, anonymized
- Data deletion API available: removes all records for a given anon_hash
