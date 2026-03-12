# Why WhatsApp?

## The Access Problem

Building a native app for rural India means:
- User must find the app in a store (assumes literacy + familiarity)
- User must download it (assumes stable internet + storage space)
- User must create an account (assumes email or comfort with registration)
- User must learn a new interface while feeling unwell

Each step is a dropout point. In our field interviews, most rural users had 2-3 apps on their phone: WhatsApp, a payment app, and sometimes YouTube.

## WhatsApp as Infrastructure

- 500M+ users in India alone
- Works on 2G networks
- Pre-installed on most smartphones
- Familiar interface across age groups and literacy levels
- Supports text, voice messages, and images natively
- End-to-end encrypted by default

## Our Approach

The patient sends a WhatsApp message to SYMTHO's number. That's it. No download, no account, no learning curve.

Voice messages are especially important — many rural users are more comfortable speaking than typing, and some have limited literacy. Our speech-to-text pipeline handles Hindi and English with regional dialect support.

## Trade-offs We Accept

- Limited UI control (no custom buttons, limited formatting)
- Dependent on Meta's platform (mitigated by messaging abstraction layer)
- Message catalog constraints (38 predefined message templates)
- No push notifications without 24h window

These are acceptable trade-offs for reaching 3B+ people who will never download a health app.
