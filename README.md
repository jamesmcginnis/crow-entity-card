# Crow Entity Card

Crow Entity Card is a single-entity Lovelace card for Home Assistant with a **liquid-glass** look and feel. Point it at any entity and choose one of three layouts: a slim **Live Activity** pill, a **Tile** that fills with the value, or a square **Glass Dial**. Tap the card to open a bottom sheet with the entity's history graph, and long-press it for optional AI tools.

> 🎨 **Built to stay readable.** State-aware colours change with the entity. Any colour you pick is adjusted automatically so it stays legible in both light and dark themes.

> ✨ **AI features are optional and off by default.** To unlock them, turn on **Enable AI features** in the AI Features section of the card editor. They need a Google Gemini conversation agent (see [AI Features Setup](#-ai-features-setup-optional) below). With AI off, everything else in the card works as normal.

**Add the repository to HACS:**

[![Open your Home Assistant instance and add this repository to HACS.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=jamesmcginnis&repository=crow-entity-card&category=plugin)

---

## 🛠️ Installation

### Via HACS (Recommended)

1. Click the **Add to HACS** button above. Alternatively, in Home Assistant open **HACS** → **⋮ menu** (top right) → **Custom repositories**
2. Add `https://github.com/jamesmcginnis/crow-entity-card` as a **Dashboard** repository, then close
3. Search for **Crow Entity Card** and click **Download**
4. Hard-refresh your browser (Cmd+Shift+R on Mac), or close and reopen the Home Assistant app on your phone
5. Edit a dashboard, click **+ Add Card** and search for **Crow Entity Card**

> 💡 HACS adds the dashboard resource for you, so there's nothing else to set up.

### Manual

1. Download `crow-entity-card.js` from [Releases](../../releases/latest)
2. Copy it into `/config/www/` on your Home Assistant instance
3. Go to **Settings → Dashboards → ⋮ menu → Resources → + Add Resource**
4. Enter `/local/crow-entity-card.js`, choose **JavaScript module** and click **Create**
5. Hard-refresh your browser and add the **Crow Entity Card** to a dashboard

---

## 🤖 AI Features Setup (Optional)

AI features are **off by default**, and the card works fully without them. To unlock them (Insight, Ask AI, What happened? and This week), turn on **Enable AI features** in the card editor's **AI Features** section, then set up Google Gemini as your conversation agent:

### Step 1 — Enable the Generative Language API

1. Go to [console.cloud.google.com](https://console.cloud.google.com) and sign in
2. Create a new project (or select an existing one)
3. Go to **APIs & Services → Library**
4. Search for **Generative Language API** and click **Enable**

> ⚠️ This step is essential. An API key without the Generative Language API enabled will return errors immediately.

### Step 2 — Create an API Key

1. In Google Cloud Console go to **APIs & Services → Credentials**
2. Click **+ Create Credentials → API key** and copy the key

### Step 3 — Add Google Generative AI to Home Assistant

1. In Home Assistant go to **Settings → Devices & Services → + Add Integration**
2. Search for **Google Generative AI** and select it
3. Paste your API key and click Submit
4. Click the **gear icon ⚙️** next to **Google AI Conversation**
5. Uncheck **Recommended model settings**, select a current **Flash** model and save

### Step 4 — Configure the Card

1. In the card's visual editor, open the **AI Features** section and turn on **Enable AI features**
2. Select **Google AI Conversation** from the **Conversation agent** dropdown
3. Optionally, switch off any individual AI tool you don't want

AI stays off until an agent is chosen. Nothing is sent to Gemini until you open one of the AI sheets, and nothing runs in the background.

### Free Tier

Gemini's free tier is generous for a single-entity card. Answers are cached, so opening the same sheet again shortly afterwards doesn't use extra requests. Insight and Ask AI answers are kept for 10 minutes and What happened? summaries for 30 minutes. If you see a rate-limit error, your daily quota has run out and will reset the next day.

---

## ✨ Features

### Layouts

- 💊 **Live Activity**: one slim row with the icon, name, value and a "time ago" pill
- 🟧 **Tile**: a compact tile that fills with the value, like a level gauge
- ⭕ **Glass Dial**: a square card with a ring for the value, plus Min and Max chips

### Card

- 🔌 **Any entity**: sensors, binary sensors, lights, switches, fans, covers, locks, climate, media players, people and more
- 🖼️ **Your own icon**: pick any Home Assistant (Material Design Icons) icon, or use the icon Home Assistant shows for the entity. That icon can also follow the entity's state.
- 🏷️ **Friendly binary states**: doors show Open / Closed, motion shows Detected / Clear, moisture shows Wet / Dry, and so on
- 🔢 **Number formatting**: choose 0–3 decimal places, or Auto, which drops trailing zeros
- 📏 **Range**: set a minimum and maximum to fill the Tile and the Dial's ring. Percentages fill 0–100 automatically.
- 👆 **Tap action**: open the details sheet, toggle the entity, or do nothing
- ✋ **Long-press**: opens the actions sheet when AI features are on, or otherwise the details sheet

### Details Sheet

- 📈 **History graph**: a line graph for numeric entities, or an on/off timeline for things that switch
- ⏱️ **1h, 3h, 6h, 12h or 24h** ranges, with your choice of which opens first
- 👉 **Tap-or-drag readout**: a glass pill shows the exact value and time anywhere along the graph
- 📊 **On-time summary**: for on/off entities, how long it was on and what percentage of the period that was
- 🔘 **Toggle or Lock / Unlock** button for entities that support it

### Appearance

- **Theme**: Auto (follows your Home Assistant theme), Light or Dark
- **Glass slider**: from Clear to Frosted. It looks best over a wallpaper or coloured view.
- **Size**: Compact, which matches standard widget sizing, or Regular, which is about 20% larger
- **Animations**: Subtle, Full, Off, or System (Subtle, but stays still when your device's Reduce Motion setting is on)
- **Colour presets**: Ember, Ocean, Berry and Graphite, plus custom Active, Icon and Graph colours
- **State colours**: the icon and glow use the Active colour when on and go neutral when off. Colours are adjusted automatically to stay readable in both light and dark themes.

### AI Features

These are all optional, and each one can be switched off individually in the editor. Long-press the card to open them:

- **Insight**: what the current state or reading means, with a practical tip
- **Ask AI**: type a question about the entity, or tap a suggested one
- **What happened?**: the latest activity as a timeline, or the last 24 hours for a sensor, with a short summary
- **This week**: seven days of history as a few key numbers, with a short summary

> 🔒 **The AI only works with facts from Home Assistant.** Each request includes the entity's actual state and history, and the AI is told not to add anything that isn't in that data.

---

## 📋 Quick Start

```yaml
type: custom:crow-entity-card
entity: sensor.living_room_temperature
layout: pill
appearance: auto
glass: 50
size: compact
animation: subtle
tap_action: popup
graph_hours: 3
state_color: true
active_color: '#FF9F0A'
icon_color: '#34C759'
graph_color: '#0A84FF'
ai_features_enabled: true
ai_conversation_agent: conversation.google_generative_ai
ai_enable_insight: true
ai_enable_ask: true
ai_enable_recap: true
ai_enable_week: true
```

> **Note:** Everything above can be set from the visual editor. AI features are **off by default**. The example above enables them; leave `ai_features_enabled` out (or set it to `false`) for a card with no AI. Your Gemini agent's entity ID may differ, so pick it from the editor's dropdown.

### Configuration Options

| Option | Default | Description |
|--------|---------|-------------|
| `entity` | *(required)* | The entity to show |
| `layout` | `pill` | `pill` (Live Activity), `tile` or `dial` |
| `name` | *(entity name)* | Custom name for the card |
| `show_name` | `true` | Show the name on the card |
| `icon` | *(entity icon)* | Any `mdi:` icon |
| `use_dynamic_icon` | `false` | Use the entity's own state-aware icon, even if an icon is set |
| `unit` | *(entity unit)* | Custom unit |
| `decimals` | *(auto)* | `0` to `3` decimal places for numeric values |
| `min` | — | Bottom of the range for the Tile and Dial fill |
| `max` | — | Top of the range for the Tile and Dial fill |
| `tap_action` | `popup` | `popup` (details sheet), `toggle` or `none` |
| `graph_hours` | `3` | History range opened first: `1`, `3`, `6`, `12` or `24` |
| `appearance` | `auto` | `auto`, `light` or `dark` |
| `glass` | `50` | Glass transparency, `0` (clear) to `100` (frosted) |
| `size` | `compact` | `compact` or `regular` |
| `animation` | `subtle` | `subtle`, `full`, `off` or `system` |
| `state_color` | `true` | Icon and glow change with the state |
| `active_color` | `#FF9F0A` | Colour when on, open or playing, or when it has a value |
| `icon_color` | `#34C759` | Fixed icon colour, used when `state_color` is off |
| `graph_color` | `#0A84FF` | History graph line |
| `ai_features_enabled` | `false` | Master switch for all AI features |
| `ai_conversation_agent` | — | Your Google Gemini conversation agent |
| `ai_enable_insight` | `true` | Insight |
| `ai_enable_ask` | `true` | Ask AI |
| `ai_enable_recap` | `true` | What happened? |
| `ai_enable_week` | `true` | This week |

---

## 🔧 Troubleshooting

**The card doesn't appear in the card picker**
- Hard-refresh your browser, or close and reopen the Home Assistant app on your phone.
- For manual installs, check `/local/crow-entity-card.js` is listed under **Settings → Dashboards → Resources** as a **JavaScript module**.

**The glass looks solid**
- Glass needs something behind it to show through. Use a dashboard wallpaper or a coloured view, and move the **Glass** slider towards Clear.

**There's no history graph in the details sheet**
- Graphs are shown for numeric entities and on/off entities. Text-only states (such as a weather condition) show their details without a graph.
- If the graph says there's no history, check the entity isn't excluded from Home Assistant's **Recorder**.

**Tapping doesn't toggle the entity**
- Set **When the card is tapped** to **Toggle** in the editor. Toggle only works for entities that can be switched, such as lights, switches, fans, covers and locks.

**AI features are missing, or long-press only opens the details sheet**
- Check **Enable AI features** is turned on in the editor's **AI Features** section. AI is off by default.
- Confirm **Google AI Conversation** is selected as the **Conversation agent**. AI stays off until one is chosen.
- Ensure the **Generative Language API** is enabled in Google Cloud Console. This is the most common setup mistake.

**Custom colours don't seem to apply exactly**
- Colours are adjusted automatically to stay readable. The "Aa" swatches in the editor preview each colour on a dark and a light card.

---

## 🙏 Credits & Acknowledgements

- The [Home Assistant](https://www.home-assistant.io) team
- The HA community for inspiration and feedback
- All users who test, report issues and suggest improvements
- My Loving Wife for her endless support ❤️

---

## 📄 License

MIT License: free to use, modify and distribute.

---

## ⭐ Support

If this is useful to you, please **star the repository** and share it with the community!

For bugs or feature requests, use the [GitHub Issues](../../issues) page.
