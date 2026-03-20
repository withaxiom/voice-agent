# Pest Control Demo

**AI Receptionist: Sam** — A bilingual (EN/ES) voice agent for pest control companies.

Answers calls 24/7, identifies the pest problem, assesses urgency, checks service area, and books appointments — without a human touching the phone.

## Why Pest Control

| Stat | Impact |
|------|--------|
| Average missed call | $150-500 in lost revenue |
| Peak season call volume | 200+ calls/day |
| Calls missed during busy hours | 20-30% |
| After-hours calls to voicemail | ~0% conversion |

Pest control is a **high-volume, time-sensitive** vertical. Customers who call about roaches or rodents want help *now* — if they hit voicemail, they call the next company.

## Call Flow

```
Caller: "I've been seeing roaches in my kitchen"
         |
         v
Sam identifies pest type + severity
         |
         v
Sam checks urgency (health risk? children? allergies?)
         |
         v
Sam verifies service area (zip code)
         |
         v
Sam books next available appointment
         |
         v
Lead logged with full details
```

## Demo Talk Track (60 seconds)

1. **"Watch — I'm going to call this pest control company at 2am."**
2. Phone rings once. Sam answers immediately.
3. **"I've been seeing roaches in my kitchen for about a week."**
4. Sam asks follow-ups, checks availability, books appointment.
5. **"That was AI. It just booked a real appointment, logged the lead, and will send a text reminder. The owner didn't have to lift a finger."**

## Setup

This demo uses the same Vapi.ai infrastructure as the law firm demo.

1. Set up the backend following [`../voice-agent/README.md`](../voice-agent/README.md)
2. Copy `system_prompt.txt` into your Vapi assistant config
3. Update the system prompt with the client's:
   - Company name (replace "GreenShield Pest Control")
   - Service area zip codes
   - Pricing and warranty terms
   - Business hours

## Customization Checklist

- [ ] Company name and branding
- [ ] Service area (zip codes)
- [ ] Pricing (free inspection vs. paid initial visit)
- [ ] Warranty terms (30/60/90 day guarantee)
- [ ] Business hours and emergency availability
- [ ] Voice selection (ElevenLabs voice ID)
- [ ] CRM integration (where leads get logged)
- [ ] SMS confirmation setup

## Pricing Guide

| Package | Price | Includes |
|---------|-------|----------|
| **Pilot** | $500 | 3-5 day setup, money-back guarantee, basic prompt + phone number |
| **Full Integration** | $1,500-2,500 | CRM integration, scheduling sync, SMS confirmations, custom voice |
| **Retainer** | $200-500/mo | Ongoing optimization, prompt tuning, analytics, support |

---

Built by **[AXIOM Collective](https://withaxiom.co)** — AI voice agents for service businesses. Bilingual (EN/ES) by default.
