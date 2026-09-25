# Logistics Voice Agent

A voice-first package-tracking assistant.

It validates shipment IDs, calls a logistics API, returns status clearly, and refuses unauthorized commitments (for example refund promises).

**Live:** https://minacava.github.io/logistics-voice-agent/

## Try it

Open the live page, allow the microphone, then:

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

Static page (`index.html`) hosting the public voice widget.

## Author

Marina Camacho
