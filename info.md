# Crow Entity Card

Crow Entity Card is a single-entity Lovelace card for Home Assistant with a **liquid-glass** look and feel. Point it at any entity and choose one of three layouts: a slim **Live Activity** pill, a **Tile** that fills with the value, or a square **Glass Dial**. Tap the card for a bottom sheet with the entity's history graph.

> ✨ **AI features are optional and off by default.** To unlock them, turn on **Enable AI features** in the editor's AI Features section. They need a Google Gemini conversation agent. With AI off, everything else in the card works as normal.

## Key Features

- **Three Layouts**: Live Activity, Tile and Glass Dial
- **Any Entity**: sensors, lights, switches, doors, locks, climate, media players and more
- **Your Own Icon**: any Home Assistant icon, or the entity's own state-aware icon
- **Friendly States**: Open / Closed, Detected / Clear, Wet / Dry and more for binary sensors
- **Range Fill**: set a minimum and maximum to fill the Tile and the Dial's ring
- **Details Sheet**: a history graph or on/off timeline from 1 to 24 hours, with a tap-or-drag readout
- **Tap and Long-press**: open details, toggle the entity, or open the AI actions sheet
- **Glass Style**: Auto, Light or Dark theme with a Clear-to-Frosted slider
- **Compact or Regular Size**: Compact matches standard widget sizing
- **Animations**: Subtle, Full, Off or System (respects your device’s Reduce Motion setting)
- **Colour Presets**: Ember, Ocean, Berry and Graphite, plus custom colours that stay readable in light and dark

## AI Features

These are all optional, and each one can be switched off individually. Long-press the card to open them:

- **Insight**: what the current state or reading means, with a practical tip
- **Ask AI**: plain-English questions about the entity
- **What happened?**: the latest activity as a timeline, with a short summary
- **This week**: seven days of history as a few key numbers, with a short summary

To set up Google Gemini, enable the **Generative Language API** in Google Cloud Console and add the **Google Generative AI** integration with your API key. Then select **Google AI Conversation** as the card's Conversation agent. Full step-by-step setup is in the README.

## Installation

1. Add `https://github.com/jamesmcginnis/crow-entity-card` as a **Dashboard** custom repository in HACS
2. Search for **Crow Entity Card** and click **Download**
3. Hard-refresh your browser, or close and reopen the HA app on your phone
4. Add the **Crow Entity Card** to a dashboard

To install manually instead, copy `crow-entity-card.js` from the [Releases](../../releases/latest) page into `/config/www/`. Then add `/local/crow-entity-card.js` as a **JavaScript module** resource.

## Quick Start

```yaml
type: custom:crow-entity-card
entity: sensor.living_room_temperature
layout: pill
appearance: auto
glass: 50
ai_features_enabled: true
ai_conversation_agent: conversation.google_generative_ai
```

> **Note:** Everything above can be set from the visual editor. AI features are **off by default**. The example above enables them; leave `ai_features_enabled` out (or set it to `false`) for a card with no AI.
