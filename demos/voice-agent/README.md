# Law Firm Demo — "Alex"

The full runnable voice agent demo. Alex is a bilingual (EN/ES) AI receptionist that qualifies law firm leads via phone calls.

## Call Flow

```
Caller dials in
      |
      v
Alex answers instantly (EN or ES)
      |
      v
Asks 5 qualifying questions
      |
      v
Scores the lead (0-10)
      |
      v
  +--------+--------+--------+
  | 7-10   | 4-6    | 1-3    |
  | QUAL.  | NURT.  | REDIR. |
  +--------+--------+--------+
  | Books  | Sends  | Refers |
  | consult| email  | to aid |
  +--------+--------+--------+
      |
      v
Lead logged -> dashboard
```

## Scoring Rubric

| # | Question | Max Points |
|---|----------|-----------|
| 1 | Type of legal matter | 2 pts |
| 2 | Timeline / urgency | 2 pts |
| 3 | Other attorneys consulted | 2 pts |
| 4 | Readiness to proceed | 2 pts |
| 5 | Jurisdiction / zip code | 2 pts |
| | **Total** | **10 pts** |

## Project Structure

```
demos/voice-agent/
├── server.py              # Flask: webhooks + dashboard + auth + admin
├── vapi_setup.py          # One-command Vapi provisioning
├── prompts/
│   └── system_prompt.txt  # Alex's personality + scoring rubric
├── requirements.txt
├── .env.example
└── docs/plans/            # Architecture documentation
```

## Setup

### 1. Install

```bash
cd demos/voice-agent
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### 2. Configure

```bash
cp .env.example .env
```

Edit `.env` with your keys:

```env
VAPI_API_KEY=your_vapi_key          # dashboard.vapi.ai > API Keys
RESEND_API_KEY=your_resend_key      # resend.com > API Keys
SECRET_KEY=any_random_string        # Flask session secret
```

Add your **ElevenLabs API key** in the Vapi dashboard: **Settings > Integrations**.

### 3. Start the server

```bash
python server.py
```

Server runs on `http://localhost:5002`.

### 4. Start ngrok

```bash
ngrok http 5002
```

Copy the `https://` URL.

> First time? Sign up at [ngrok.com](https://dashboard.ngrok.com) and run `ngrok config add-authtoken YOUR_TOKEN`.

### 5. Set up Vapi

```bash
python vapi_setup.py setup
```

Paste your ngrok URL when prompted. This creates:
- 4 tools: `log_lead`, `check_availability`, `send_nurture_email`, `transfer_call`
- The assistant (Claude + ElevenLabs + Deepgram)
- A phone number (830 area code)

### 6. Test

Call the phone number. After the call, check `http://localhost:5002` for the logged lead.

### 7. Create admin user (optional)

```bash
python server.py create-admin
```

Unlocks: user management, cost analysis dashboard, lead deletion.

## Dashboard Features

- **Lead table** with color-coded scores (green/yellow/red)
- **Live stats** — total, qualified, nurture, redirect counts
- **Auto-refresh** every 10 seconds
- **Search** by name, phone, or email
- **Filter** by routing type or status
- **Lead detail view** — full case summary, notes, status workflow
- **Browser notifications** for new qualified leads

### Roles

| Role | Can do |
|------|--------|
| **Admin** | Everything + manage users + delete leads + cost analysis |
| **Attorney** | View all leads + add notes + change lead status |
| **Staff** | View all leads + add notes |

## API

### `GET /api/leads`

```bash
curl http://localhost:5002/api/leads
```

Returns all leads as JSON, most recent first.

### `POST /webhook/tools`

Vapi sends tool calls here (`log_lead`, `check_availability`, `send_nurture_email`, `transfer_call`).

### `POST /webhook/vapi`

End-of-call reports from Vapi (call duration tracking).

## Vapi Management

```bash
python vapi_setup.py status     # See what's deployed
python vapi_setup.py teardown   # Delete everything
python vapi_setup.py setup      # Re-deploy with new ngrok URL
```

## Troubleshooting

| Problem | Fix |
|---------|-----|
| No voice on call | Add ElevenLabs key in Vapi > Settings > Integrations |
| No leads appearing | Both Flask + ngrok must be running. URLs must match. |
| Emails not sending | Check `RESEND_API_KEY`. Free tier only sends to signup email. |
| ngrok auth error | `ngrok config add-authtoken YOUR_TOKEN` |
| 500 on tool calls | Check Flask logs. Vapi uses `parameters` key (server handles both). |
| Restarted ngrok | Re-run `python vapi_setup.py setup` with new URL |

## Tech Stack

| Component | Service |
|-----------|---------|
| Voice Platform | [Vapi.ai](https://vapi.ai) |
| AI Model | Claude Sonnet (Anthropic) |
| Voice | ElevenLabs |
| Transcription | Deepgram Nova 2 |
| Backend | Flask (Python) |
| Email | Resend |
| Database | SQLite |
| Auth | Google OAuth + email/password |
| Tunnel | ngrok |

---

Built by **[AXIOM Collective](https://withaxiom.co)** — AI voice agents for service businesses.
