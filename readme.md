# ⚡ Storyverse — Harry Potter Character Conversations

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

## Design Decisions

**Why separate HTML files instead of one app?**
Each book pair is a self-contained ~25-30KB HTML file with zero dependencies. This means instant loading, no build step, no framework overhead, and each file works independently. A single combined file exceeded browser rendering limits due to the volume of chapter event data (199 chapters × event arrays).

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

## About

Built as a product + AI engineering portfolio project exploring how fictional characters can be made canonically accurate, emotionally responsive, and theatrically engaging through prompt architecture.

---

## License

MIT — see [LICENSE](./LICENSE) for details.

The character names, events, and world of Harry Potter are the intellectual property of J.K. Rowling and Warner Bros. This project is a fan-made, non-commercial portfolio piece. No copyrighted text is reproduced — all chapter event data is original summarization.
