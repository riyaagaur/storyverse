# ⚡ Storyverse — Harry Potter Character Conversations

An AI-powered, chapter-accurate character chatbot system where you can talk to Harry Potter characters — and they only know what they'd know at your exact point in the story.

**[🔮 Live Demo →](https://yourusername.github.io/storyverse)**

---

## What This Is

Select a book. Choose how far you've read. Pick a character. You're dropped mid-scene into a conversation where the character's knowledge, personality, and emotional state are scoped precisely to your chapter.

Tell Ron about Horcruxes at Chapter 3? He's genuinely confused. Push Snape too hard? He shuts down entirely. Be kind to Neville across five turns? He opens up about things he normally won't mention.

No other character AI product combines canonical IP fidelity, chapter-level knowledge boundaries, emotional state tracking, and theatrical scene-driven responses.

---

## Features

### Core Architecture
- **Chapter-wise knowledge boundaries** — 199 chapters across all 7 books. Each character's knowledge is scoped to exactly what has happened up to your selected chapter. No foreshadowing, no leakage, no dramatic irony.
- **Public vs private context** — characters freely discuss events they know, but protect secrets the way they would in the story. Snape's love for Lily shapes every response. He will never tell you.
- **Future knowledge resistance** — keyword + semantic pattern detection flags spoilers before the API call. Characters react with genuine in-character confusion, never system refusals.

### Engagement Systems
- **Sorting Ceremony** — a conversational 5-question sorting conducted by the Sorting Hat as a full AI character. Your house persists and changes how every character treats you.
- **Emotional state engine** — 6-level trust system (shut down → guarded → cautious → neutral → trusting → bonded). Characters self-evaluate trust each turn. Visible as avatar glow and trust pips.
- **Multi-character scenes** — when you talk to Harry, Ron and Hermione are present and react. Characters disagree. You sit in the middle of tension, not a one-on-one interview.
- **Action beat system** — 10-state physical vocabulary per character mapped to emotions. No repeat beats within a conversation. One action beat at the start of each response, then dialogue flows.

### Technical
- **Session persistence** — conversations survive page refresh, keyed by character + chapter.
- **Context compression** — after 14 messages, older exchanges are summarized to keep the context window sharp.
- **Voice drift correction** — character-specific reminders injected every 6 turns.
- **Streaming responses** — token-by-token rendering for immersive feel.

---

## Books & Characters

| Book | Chapters | Characters |
|------|----------|------------|
| Sorcerer's Stone | 17 | Harry, Ron, Hermione, Hagrid, Dumbledore, Snape, Draco, Neville + 5 CoS shared |
| Chamber of Secrets | 18 | + Dobby, Ginny, Tom Riddle, Moaning Myrtle, Lockhart |
| Prisoner of Azkaban | 22 | + **Sirius Black**, **Remus Lupin** |
| Goblet of Fire | 37 | + **Cedric Diggory**, **Mad-Eye Moody** |
| Order of the Phoenix | 38 | + **Luna Lovegood**, **Dolores Umbridge** |
| Half-Blood Prince | 30 | + **Horace Slughorn**, Tom Riddle (Pensieve) |
| Deathly Hallows | 36 | + **Aberforth Dumbledore**, **Lord Voldemort** |
| **Total** | **199** | **40+ unique character profiles** |

---

## Try It

### Live Demo
Visit **[yourusername.github.io/storyverse](https://yourusername.github.io/storyverse)** — no setup required.

### Run Locally
```bash
git clone https://github.com/yourusername/storyverse.git
cd storyverse
# Open any HTML file directly in a browser
open index.html
```

> **Note:** The chatbot requires a Claude API key. In the live demo, API calls are handled client-side. For production deployment, move API calls to a backend proxy.

---

## Repository Structure

```
storyverse/
├── README.md
├── LICENSE
├── index.html                  ← Landing page — links to all books
│
├── books/
│   ├── sorcerers-stone.html    ← Books 1 & 2 (SS + CoS)
│   ├── prisoner-of-azkaban.html← Books 3 & 4 (PoA + GoF)
│   ├── order-of-the-phoenix.html← Books 5 & 6 (OotP + HBP)
│   └── deathly-hallows.html    ← Book 7 (DH)
│
├── presentation/
│   └── index.html              ← Interactive project presentation
│
└── docs/
    ├── PRD.md                  ← Product Requirements Document
    ├── architecture.md         ← Prompt system deep-dive
    └── screenshots/
        ├── sorting.png
        ├── chat.png
        └── trust.png
```

---

## Architecture

### Prompt Construction (Runtime)
Every API call assembles a system prompt from four layers:

```
┌─────────────────────────────────────┐
│  Layer 1: Character Profile         │
│  personality · speech · triggers    │
│  physical vocabulary · private ctx  │
├─────────────────────────────────────┤
│  Layer 2: Chapter Knowledge         │
│  cumulative events Ch.1 → selected  │
│  explicit future chapter lock       │
├─────────────────────────────────────┤
│  Layer 3: Scene Context             │
│  location · user name · house       │
│  companion characters · trust level │
├─────────────────────────────────────┤
│  Layer 4: Conversation Rules        │
│  40-80 words · action beat format   │
│  hook ending · voice drift check    │
└─────────────────────────────────────┘
```

### Message Pipeline
```
User types → sanitize(future knowledge check)
          → buildSys(prompt assembly)
          → API call (streaming)
          → parseTrust(extract [T:N] tag)
          → trackBeat(log action beat)
          → render + save session
```

### Emotional State Engine
```
[0] Shut Down ← push too hard
[1] Guarded   ← default for Snape, Draco, Voldemort
[2] Cautious  ← default for Sirius, Aberforth
[3] Neutral   ← default for most characters
[4] Trusting  ← default for Dobby, Lockhart
[5] Bonded    ← earned through sustained kindness
```

Characters self-evaluate trust via a hidden `[T:N]` tag each turn. The tag is parsed and stripped before display.

---

## Design Decisions

**Why separate HTML files instead of one app?**
Each book pair is a self-contained ~25-30KB HTML file with zero dependencies. This means instant loading, no build step, no framework overhead, and each file works independently. A single combined file exceeded browser rendering limits due to the volume of chapter event data (199 chapters × event arrays).

**Why client-side API calls?**
This is a portfolio prototype, not a production deployment. Client-side calls allow instant demo without backend infrastructure. For production, API calls should be proxied through a backend service.

**Why Claude Sonnet over GPT-4?**
Sonnet follows complex multi-layered system prompts (character + chapter + trust + rules) with higher fidelity than alternatives tested. The character voice consistency and knowledge boundary adherence were measurably better in blind evaluation.

**Why not RAG over the book text?**
RAG retrieves passages — characters don't speak in passages. The chapter event lists are curated summaries of what happened, not extracted text. This gives the model the facts without copying copyrighted material, and lets characters reference events the way a person references their own life: obliquely, emotionally, in fragments.

---

## What Makes This Different

| Feature | Character.AI | Chai AI | This System |
|---------|-------------|---------|-------------|
| Knowledge boundary | None | None | Chapter-level (199 chapters) |
| Private context | None | Partial | Full (all 40+ characters) |
| Future knowledge resistance | None | None | Keyword + semantic patterns |
| Emotional state tracking | None | None | 6-level trust engine |
| Action beat system | Partial | Yes | 10-state physical vocabulary |
| Multi-character scenes | None | None | Companion disagreement |
| Sorting Ceremony | N/A | N/A | Conversational, affects all interactions |
| Session persistence | None | None | Cross-refresh, per character |
| Voice drift correction | None | None | Every 6 turns, character-specific |

---

## Tech Stack

- **Frontend:** Vanilla HTML/CSS/JS — zero dependencies, zero build step
- **AI Model:** Claude Sonnet (Anthropic API) with streaming
- **Storage:** Browser persistent storage API for sessions, trust, and user profile
- **Design:** Custom dark fantasy theme with CSS variables, particle canvas, house-adaptive colors

---

## Future Roadmap

- [ ] Backend API proxy for production deployment
- [ ] Self-evaluation benchmark (adversarial prompt testing)
- [ ] Conversation analytics dashboard
- [ ] The Daily Prophet — AI-generated chapter-specific newspaper
- [ ] Voice output integration

---

## About

Built as a product + AI engineering portfolio project exploring how fictional characters can be made canonically accurate, emotionally responsive, and theatrically engaging through prompt architecture.

The system is designed to be title-agnostic — the architecture works for any fiction with chapters and characters. Harry Potter is the reference implementation.

**Built by [Your Name]** — [LinkedIn](https://linkedin.com/in/yourprofile) · [Portfolio](https://yoursite.com)

---

## License

MIT — see [LICENSE](./LICENSE) for details.

The character names, events, and world of Harry Potter are the intellectual property of J.K. Rowling and Warner Bros. This project is a fan-made, non-commercial portfolio piece. No copyrighted text is reproduced — all chapter event data is original summarization.
