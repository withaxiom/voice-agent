# Demos

This directory contains ready-to-use voice agent demos for different business verticals.

## Available Demos

| Demo | Directory | Status | Description |
|------|-----------|--------|-------------|
| **Law Firm** | [`voice-agent/`](voice-agent/) | Full app (runnable) | AI receptionist "Alex" — qualifies legal leads, scores 0-10, books consults |
| **Pest Control** | [`pest-control/`](pest-control/) | Prompt only | AI receptionist "Sam" — identifies pest problems, books appointments |

## How the Demos Relate

- **`voice-agent/`** is the full working application — Flask server, dashboard, Vapi setup script, auth system. Start here.
- **`pest-control/`** is a system prompt that plugs into the same infrastructure. It shows how to adapt the agent for a different vertical without changing the backend.

## Running a Demo

```bash
# Start with the law firm demo (it has the full backend)
cd voice-agent/
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env  # add your API keys
python server.py      # starts on :5002
```

See [`voice-agent/README.md`](voice-agent/README.md) for the complete setup guide.

## Adding a New Vertical

1. Create a new directory: `demos/your-vertical/`
2. Copy and customize the system prompt from `voice-agent/prompts/system_prompt.txt`
3. Update qualifying questions, scoring rubric, and routing logic
4. Paste the new prompt into Vapi assistant config (or update `vapi_setup.py`)
5. Add a `README.md` with the vertical-specific demo script and talking points

## Demo Talk Track (60-90 seconds)

Use this for Loom recordings or live sales demos:

| Timing | What to do |
|--------|------------|
| **0-10s** | Hook: "Most businesses miss 20-30% of their calls. Every missed call is a lost customer." |
| **10-40s** | Call the number on speaker. Let the AI answer. Have a natural conversation. |
| **40-55s** | Reveal: "That was AI. It scored me, qualified me, and is booking a consult right now." |
| **55-70s** | Open the dashboard. Show the lead that just appeared with score and routing. |
| **70-85s** | Close: "24/7. English and Spanish. No training, no sick days. Want this for your business?" |

## Test Scenarios

### Qualified Lead (score 7-10)
> "I was in a car accident last week. A friend recommended I call. I need help as soon as possible. I'm in Eagle Pass, zip 78852."

### Nurture Lead (score 4-6)
> "My spouse and I separated about four months ago. I talked to one other attorney but I'm still figuring things out. I'm in Del Rio, 78840."

### Redirect (score 1-3)
> "My landlord kept my security deposit over a year ago. I've talked to a couple lawyers but they said they couldn't help. I'm in Dallas, 75201."
