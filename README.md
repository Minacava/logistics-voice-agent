# Logistics Voice Agent

A small personal demo of a voice-first package-tracking assistant.

The agent validates shipment IDs, calls a mock logistics API, returns status clearly, and refuses unauthorized commitments (for example refund promises).

**Live demo:** https://minacava.github.io/logistics-voice-agent/

## Try it

Open the live demo, allow the microphone, then:

| Input | Expected behavior |
| --- | --- |
| `FE-2026` | Returns delayed status, location, and ETA |
| `FE-9999` | Shipment not found — no invented data |
| `ABC-12` | Invalid format — rejected before the API call |
| “I want a refund” | Explains it cannot process refunds; offers a human handoff |

## Architecture

```
User (voice widget)
  → ElevenLabs Conversational AI (prompt + tool)
    → Beeceptor mock API POST /shipment
```

- **ElevenLabs** owns conversation, ID validation, tone, and safety rails.
- **Tool `check_shipment`** is a thin `POST` with `order_id` only.
- **Beeceptor** owns success (`FE-2026` → 200) and catch-all 404.

## Stack

- ElevenLabs Conversational AI + Convai widget embed
- Beeceptor mock HTTP endpoint

## Repo

Static page only (`index.html`) for the public widget embed.

## Author

Marina Camacho
