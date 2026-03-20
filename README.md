[![Vapi.ai](https://img.shields.io/badge/Voice-Vapi.ai-6C47FF?style=flat-square&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0IiBmaWxsPSJ3aGl0ZSI+PGNpcmNsZSBjeD0iMTIiIGN5PSIxMiIgcj0iMTAiLz48L3N2Zz4=)](https://vapi.ai)
[![Claude](https://img.shields.io/badge/AI-Claude_Sonnet-D97706?style=flat-square&logo=anthropic&logoColor=white)](https://anthropic.com)
[![ElevenLabs](https://img.shields.io/badge/Voice-ElevenLabs-000000?style=flat-square)](https://elevenlabs.io)
[![Deepgram](https://img.shields.io/badge/STT-Deepgram-13EF93?style=flat-square)](https://deepgram.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](LICENSE)
[![Bilingual](https://img.shields.io/badge/Languages-EN_%7C_ES-red?style=flat-square)]()

<br />

<h1 align="center">AXIOM Voice Agent</h1>

<p align="center">
  <strong>An AI receptionist that answers every call, qualifies every lead, and never takes a day off.</strong>
</p>

<p align="center">
  Bilingual (EN/ES) &bull; 24/7 &bull; Lead scoring &bull; Instant routing &bull; Real-time dashboard
</p>

---

## The Problem

Small businesses lose **$1,000+ per week** in missed calls. Voicemail is a dead end — 80% of callers won't leave a message. Hiring an after-hours answering service costs $800–2,000/mo and still drops the ball.

## The Solution

AXIOM Voice Agent picks up the phone in under a second, qualifies the caller with natural conversation, scores the lead, and routes them — all before a human needs to get involved.

It works while you sleep. It works during your busiest hour. It speaks English and Spanish fluently.

---

## What It Does

```
  Caller dials your business number
              |
              v
    +---------+---------+
    |   Vapi.ai picks   |
    |   up instantly     |
    |                    |
    |  ElevenLabs voice  |
    |  Deepgram STT      |
    |  Claude brain      |
    +---------+---------+
              |
              v
    AI asks qualifying questions
    (adapts to EN or ES automatically)
              |
              v
    Scores the lead (0-10)
              |
    +---------+---------+---------+
    |         |         |         |
    v         v         v         v
  7-10      4-6       1-3      Spam
QUALIFIED  NURTURE  REDIRECT   Ended
    |         |         |
    v         v         v
  Books     Sends     Refers to
  consult   resources  free/alt
  instantly via email  resources
    |         |         |
    +----+----+----+----+
         |
         v
    Lead logged to dashboard
    (name, score, summary, recording)
```

**Every call becomes a data point.** Every lead gets the right next step. Nothing falls through the cracks.

---

## Features

| Feature | Details |
|---------|---------|
| **Instant pickup** | Answers in <1 second. No hold music. No phone tree. |
| **Bilingual (EN/ES)** | Detects language automatically, switches mid-call if needed |
| **Lead scoring** | 0-10 scale based on configurable qualifying questions |
| **Smart routing** | Qualified -> book consult. Nurture -> send resources. Redirect -> alternatives. |
| **Real-time dashboard** | See every lead the moment the call ends. Filter, search, manage. |
| **Role-based access** | Admin, Attorney, Staff roles with appropriate permissions |
| **Nurture emails** | Automatic follow-up emails for warm leads via Resend |
| **Call tracking** | Duration, transcripts, and full conversation context |
| **Cost tracking** | Built-in cost analysis dashboard for Vapi/phone/email spend |

---

## Tech Stack

| Layer | Technology | Role |
|-------|-----------|------|
| Voice Platform | [Vapi.ai](https://vapi.ai) | Call handling, orchestration |
| AI Model | [Claude Sonnet](https://anthropic.com) | Conversation, reasoning, scoring |
| Voice Synthesis | [ElevenLabs](https://elevenlabs.io) | Natural-sounding speech |
| Speech-to-Text | [Deepgram Nova 2](https://deepgram.com) | Real-time transcription |
| Backend | Flask (Python) | Webhook server, dashboard, API |
| Email | [Resend](https://resend.com) | Nurture email delivery |
| Database | SQLite | Lead storage (swap for Postgres in prod) |
| Auth | Google OAuth + email/password | Dashboard access control |

---

## Quick Start

### Prerequisites

- Python 3.9+
- [ngrok](https://ngrok.com) account (free tier works)
- [Vapi.ai](https://dashboard.vapi.ai) account
- [Resend](https://resend.com) account (optional, for nurture emails)

### 1. Clone and install

```bash
git clone https://github.com/withaxiom/voice-agent.git
cd voice-agent/demos/voice-agent

python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### 2. Configure API keys

```bash
cp .env.example .env
```

Edit `.env`:

```env
VAPI_API_KEY=your_vapi_key          # From dashboard.vapi.ai > API Keys
RESEND_API_KEY=your_resend_key      # From resend.com > API Keys
SECRET_KEY=any_random_string        # For Flask sessions
```

> **Important:** Add your ElevenLabs API key inside the Vapi dashboard at **Settings > Integrations**. This is required for the voice to work.

### 3. Start the server

```bash
python server.py
```

### 4. Expose with ngrok

In a second terminal:

```bash
ngrok http 5002
```

Copy the `https://` URL it gives you.

### 5. Set up Vapi

In a third terminal:

```bash
source .venv/bin/activate
python vapi_setup.py setup
```

Paste your ngrok URL when prompted. This creates:
- 4 webhook tools (log_lead, check_availability, send_nurture_email, transfer_call)
- The AI assistant with Claude + ElevenLabs + Deepgram
- A phone number (830 area code)

### 6. Call the number

Call it from your phone. The AI answers instantly. After the call, check the dashboard at `http://localhost:5002`.

### 7. Create a dashboard admin (optional)

```bash
python server.py create-admin
```

This gives you login access to the full dashboard with user management and cost analysis.

---

## Demo Script (60-90 seconds)

Use this script for Loom videos, live demos, or sales calls:

**Hook (10s):**
> "Most businesses miss 20-30% of their calls. Every missed call is a lost customer. Watch what happens when I call this business at 2am."

**Live call (30s):**
> Call the number on speaker. Let the AI answer. Have a natural conversation — describe a problem, answer the qualifying questions.

**Scoring (10s):**
> "That was an AI. It just qualified me as a lead, scored me 8 out of 10, and is booking a consultation right now. All in under 90 seconds."

**Dashboard (15s):**
> Open the dashboard. Point to the lead that just appeared — name, score, case summary, routing decision.

**Close (10s):**
> "This works 24/7. English and Spanish. No training, no sick days, no hold music. If you want this for your business, let's talk."

### Test Scenarios

| Scenario | What to say | Expected Score | Expected Routing |
|----------|------------|----------------|------------------|
| **Hot lead** | Personal injury, car accident last week, want to act ASAP, zip 78852 | 7-10 | QUALIFIED (books consult) |
| **Warm lead** | Considering divorce, separated 4 months, still deciding, zip 78840 | 4-6 | NURTURE (sends resources) |
| **Cold lead** | Security deposit dispute, 13 months ago, two attorneys declined, zip 75201 | 1-3 | REDIRECT (refers to Legal Aid) |

---

## Customize for Any Vertical

The voice agent is **vertical-agnostic**. The qualifying questions, scoring rubric, and routing logic all live in a single system prompt file that you swap per client.

### Included Demos

| Vertical | Directory | AI Name | What It Qualifies |
|----------|-----------|---------|-------------------|
| **Law Firm** | `demos/voice-agent/` | Alex | Case type, urgency, intent, jurisdiction |
| **Pest Control** | `demos/pest-control/` | Sam | Pest type, urgency, service area, booking |

### How to Adapt for a New Vertical

1. **Copy the system prompt** from `demos/voice-agent/prompts/system_prompt.txt`
2. **Change the qualifying questions** to match the vertical:

| Vertical | Sample Questions |
|----------|-----------------|
| **Dental** | Type of visit (cleaning/emergency/cosmetic)? Insurance? Last visit? Pain level? |
| **Legal** | Case type? Timeline? Other attorneys consulted? Ready to proceed? Jurisdiction? |
| **Pest Control** | What pest? How long? Urgency (health risk)? Service area? Preferred time? |
| **HVAC** | AC or heating? How long? Under warranty? Home or commercial? Preferred time? |
| **Real Estate** | Buying or selling? Timeline? Pre-approved? Budget range? Area? |
| **Med Spa** | Treatment interest? First time? Budget? Timeline? Consultation or booking? |

3. **Update the scoring rubric** (what makes a lead hot vs. cold for this business)
4. **Update routing logic** (what happens at each score tier)
5. **Set the personality** (name, tone, company name, business hours)
6. **Configure bilingual support** if needed (EN/ES included by default)

> **Typical customization time:** 2-4 hours for a new vertical, including testing.

---

## Project Structure

```
voice-agent/
├── README.md                           # You are here
├── demos/
│   ├── README.md                       # Demo index + Loom script
│   ├── voice-agent/                    # Law firm demo (full runnable app)
│   │   ├── server.py                   # Flask server: webhooks + dashboard + auth
│   │   ├── vapi_setup.py              # One-command Vapi provisioning
│   │   ├── prompts/
│   │   │   └── system_prompt.txt      # AI personality + scoring rubric
│   │   ├── requirements.txt
│   │   ├── .env.example
│   │   └── docs/plans/               # Architecture docs
│   └── pest-control/                  # Pest control demo (prompt only)
│       ├── README.md
│       └── system_prompt.txt          # Sam's personality + pest control flow
└── screenshots/                       # Demo screenshots
```

---

## API Reference

### `GET /api/leads`

Returns all leads as JSON (most recent first).

```bash
curl http://localhost:5002/api/leads
```

```json
[
  {
    "id": 1,
    "caller_name": "Maria",
    "case_type": "personal injury",
    "case_summary": "Car accident last week, neck and back pain...",
    "score": 9,
    "routing": "qualified",
    "email": "maria@example.com",
    "zip_code": "78852",
    "phone": "+18301234567",
    "status": "new",
    "call_duration_seconds": 142,
    "created_at": "2026-03-04T11:00:00"
  }
]
```

### `POST /webhook/tools`

Vapi sends tool calls here. Handles: `log_lead`, `check_availability`, `send_nurture_email`, `transfer_call`.

### `POST /webhook/vapi`

Receives end-of-call reports from Vapi (call duration tracking).

---

## Managing Vapi Resources

```bash
# Check what's deployed
python vapi_setup.py status

# Tear down everything (tools, assistant, phone number)
python vapi_setup.py teardown

# Re-deploy with a new ngrok URL
python vapi_setup.py setup
```

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| **Call connects but no voice** | Add your ElevenLabs API key in Vapi dashboard > Settings > Integrations |
| **No leads on dashboard** | Ensure Flask server AND ngrok are both running. ngrok URL must match what you gave `vapi_setup.py`. |
| **ngrok auth error** | Run `ngrok config add-authtoken YOUR_TOKEN` from [ngrok dashboard](https://dashboard.ngrok.com) |
| **Nurture emails not sending** | Check `RESEND_API_KEY` in `.env`. Free Resend tier only sends to your signup email. |
| **500 errors on tool calls** | Check Flask server logs. Vapi sends params under `parameters` key (server handles both formats). |
| **New ngrok URL after restart** | Re-run `python vapi_setup.py setup` with the new URL, or update it in Vapi dashboard. |

---

## What It Costs to Run

| Service | Cost | Notes |
|---------|------|-------|
| Vapi.ai | ~$0.05/min | Pay per minute of call time |
| Phone number | ~$2/mo | Provisioned through Vapi |
| ElevenLabs | Included via Vapi | Billed through Vapi's per-minute rate |
| Deepgram | Included via Vapi | Billed through Vapi's per-minute rate |
| Resend | Free tier: 100 emails/day | More than enough for most businesses |
| Hosting | ~$5-10/mo | Any VPS or cloud instance runs the Flask server |

**Total for a typical small business:** ~$20-50/mo depending on call volume.

---

<h2 align="center">Want this for your business?</h2>

<p align="center">
  <strong>AXIOM builds AI voice agents, automation workflows, and bilingual AI systems for service businesses.</strong>
</p>

<p align="center">
  We'll set up a custom voice agent for your business in 3-5 days.<br />
  Flat-rate pilot: <strong>$500</strong> (money-back guarantee).<br />
  Full integration with your CRM + scheduling: <strong>$1,500-2,500</strong>.<br />
  Ongoing optimization: <strong>$200-500/mo</strong>.
</p>

<p align="center">
  <a href="https://withaxiom.co"><strong>withaxiom.co</strong></a> &bull; Bilingual (EN/ES) by default
</p>

<p align="center">
  <em>Stop missing calls. Start closing leads.</em>
</p>
