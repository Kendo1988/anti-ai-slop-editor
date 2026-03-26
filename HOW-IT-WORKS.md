# How It Works

This document explains the detection system, scoring methodology, and rewriting principles behind the Anti AI Slop Editor skill. If you want to understand what the skill checks for and why, this is the right place.

---

## The Core Idea

AI-generated text follows predictable patterns. Not because any single pattern is proof of AI authorship, but because the same patterns appear together, repeatedly, across virtually all AI-generated content. This skill looks for those patterns, counts them, scores the text, and rewrites it to break the patterns.

The system works in both **English** and **German**.

---

## The 10-Point Mandatory Checklist

Every time the skill audits a text, it runs through all 10 checks. No check is skipped. Here is what each one does and why it matters.

### 1. Em-Dash Count

**What it checks:** The number of em-dashes ( -- and --- ) in the text.

**The rule:** Maximum 1 em-dash per paragraph. If the entire text has more than 5 em-dashes total, the skill flags it.

**Why this matters:** AI models love em-dashes. They use them as a crutch for parenthetical asides, mid-sentence pivots, and dramatic pauses. A human writer might use one occasionally. AI text is riddled with them.

**Example violation:**
> Our platform -- designed for scale -- handles millions of requests -- without breaking a sweat -- every single day.

### 2. Lists of Three (Dreier-Listen)

**What it checks:** Whether every list in the text has exactly 3 items.

**The rule:** Vary list lengths. Use 2, 4, or 5 items. If every list has exactly 3 items, the text is flagged.

**Why this matters:** AI has a strong bias toward groups of three. Three bullet points, three examples, three benefits. Real writing has irregular list lengths because real information does not always come in threes.

### 3. Triple Adjective Chains (Dreier-Adjektiv-Ketten)

**What it checks:** Sequences of three adjectives stacked before a noun.

**The rule:** One adjective is usually enough. Two if you must. Three is almost always filler.

**Why this matters:** "Our innovative, scalable, enterprise-grade solution" is a hallmark of AI writing. Each adjective adds less meaning than the last. The skill forces the writer (or the rewrite) to pick the one adjective that actually matters.

**Example violation:**
> An innovative, cutting-edge, and transformative approach to data management.

**Rewritten:**
> A faster approach to data management. (Then prove it with numbers.)

### 4. "Not only... but also" (nicht nur... sondern auch)

**What it checks:** The antithetical construction "not only X, but also Y" (and its German equivalent).

**The rule:** Just say both things directly.

**Why this matters:** This construction is AI's favorite way to sound sophisticated. It adds length without adding meaning. "We handle payments and shipping" is clearer than "We not only handle payments, but also provide comprehensive shipping solutions."

### 5. Word Frequency

**What it checks:** How often certain overused words appear. The tracked words include: "seamless", "comprehensive", "robust", "leverage", "innovative", "streamline", "empower", "foster", "holistic", "synergy" (English) and "strukturiert", "transparent", "professionell", "zuverlaessig", "systematisch", "nahtlos", "umfassend" (German).

**The rule:** Each tracked word may appear a maximum of 2 times across the entire text.

**Why this matters:** AI models reach for the same "impressive-sounding" words repeatedly. A text that uses "seamless" four times and "comprehensive" three times reads like it was generated, not written. Real writers have larger, more varied vocabularies -- or they just use plain words.

### 6. Repetitive Sentence Openers (Monotone Satzanfaenge)

**What it checks:** Whether consecutive sentences or paragraphs start with the same word or structure.

**The rule:** Vary your sentence openers. Do not start three sentences in a row with "This enables...", "This ensures...", "This provides...".

**Why this matters:** AI tends to fall into rhythmic patterns. The same opener repeated creates a droning, predictable cadence that human writers naturally avoid.

**Example violation:**
> This enables teams to collaborate faster. This ensures data consistency across regions. This provides a single source of truth.

**Rewritten:**
> Teams collaborate faster. Data stays consistent across regions. Everyone works from one source of truth.

### 7. Passive Voice Overload (Passiv-Overkill)

**What it checks:** Excessive use of passive voice, especially stacked passive constructions.

**The rule:** Use active voice. Name the actor. Say who did what.

**Why this matters:** AI defaults to passive voice because it avoids committing to a subject. "It was determined that improvements were needed" hides who determined it and what improvements. "The engineering team identified three bottlenecks" is concrete and credible.

**Example violation:**
> It was determined that a new approach was needed, and it was decided that resources would be allocated.

**Rewritten:**
> The product team decided to change the approach and assigned two engineers to the project.

### 8. Banned Words and Phrases

**What it checks:** The text is scanned against two blacklist tables -- one for English, one for German. These tables contain words and phrases that are statistically overrepresented in AI-generated text.

**The rule:** Zero tolerance. If a banned word or phrase appears, it must be replaced or removed.

**English examples of banned terms:**
| Banned | Why | Use Instead |
|---|---|---|
| delve | AI's favorite verb | examine, look at, analyze |
| landscape | almost never literal | field, market, area |
| it's worth noting | filler -- just state the thing | (delete it, state the fact) |
| at the end of the day | cliche | ultimately, in practice |
| game-changer | hyperbole | improvement, advantage |
| leverage (as verb) | corporate AI speak | use |
| empower | vague and patronizing | enable, help, let |
| seamlessly | nothing is seamless | smoothly, without errors |
| deep dive | overused metaphor | detailed look, analysis |
| robust | meaningless without context | reliable, tested, strong |

**German examples of banned terms:**
| Banned | Why | Use Instead |
|---|---|---|
| im heutigen digitalen Zeitalter | cliche opener | (delete, start with the point) |
| ganzheitlich | vague buzzword | vollstaendig, komplett |
| massgeschneidert | overused | angepasst, individuell |
| Mehrwert | says nothing specific | konkreten Nutzen benennen |
| auf das naechste Level heben | borrowed metaphor, overused | verbessern, beschleunigen |
| Synergie | corporate filler | Zusammenarbeit, Vorteil |

The full blacklists in the skill file contain many more entries.

### 9. Rhetorical Question Openers

**What it checks:** Whether the text opens with a rhetorical question.

**The rule:** Do not open with a question like "Have you ever wondered...?" or "What if there was a better way...?"

**Why this matters:** Rhetorical question openers are a lazy engagement tactic. They delay the actual content and signal that the writer (or AI) is padding for length. Start with the answer instead.

**Example violation:**
> Have you ever wondered why your deployment pipeline takes so long?

**Rewritten:**
> Your deployment pipeline is slow because it rebuilds containers from scratch on every push.

### 10. Fake Participation

**What it checks:** Phrases that create a false sense of shared activity between the writer and reader.

**The rule:** Do not use "Let's explore...", "Join us as we...", "Let's dive in...", or "Tauchen Sie ein...". The writer is writing. The reader is reading. You are not doing anything together.

**Why this matters:** This is one of the most recognizable AI writing patterns. It mimics a friendly tour guide voice that no real technical writer or blogger uses naturally.

**Example violation:**
> Let's explore how our platform transforms the way you think about data.

**Rewritten:**
> The platform organizes your data into three categories: active, archived, and flagged.

---

## The Slop Scale (0-10 Scoring)

After running all 10 checks, the skill assigns a **Slop Score** from 0 to 10. This score tells you how AI-detectable your text is.

| Score | Label | What It Means |
|---|---|---|
| 0 | Clean | No detectable AI patterns. Reads like a human wrote it with intent. |
| 1-2 | Minor traces | One or two minor patterns. Easily fixable. Most human-written text lands here. |
| 3-4 | Noticeable | Several AI patterns present. A careful reader would suspect AI involvement. |
| 5-6 | Obvious | The text has clear AI fingerprints. Multiple checklist violations. Needs a rewrite. |
| 7-8 | Heavy slop | The text is dominated by AI patterns. Banned words, passive voice, triple adjective chains, monotone structure. Significant rewrite required. |
| 9-10 | Pure slop | The text reads like raw, unedited AI output. Nearly every sentence triggers a checklist item. Full rewrite from scratch recommended. |

The score is diagnostic, not punitive. A score of 4 does not mean the text is bad -- it means there are specific, fixable patterns that make it sound machine-generated.

---

## Rewriting Principles

When the skill rewrites text, it follows these rules:

### 1. Shorter sentences win
Long, winding sentences with multiple clauses are an AI hallmark. The skill breaks them into shorter, direct statements.

### 2. Active voice over passive
"The team built the feature" instead of "The feature was built by the team." Active voice names the actor and creates momentum.

### 3. Specific over vague
Replace vague claims with concrete details. "Our platform is fast" becomes "Pages load in 200ms on a 3G connection." If there is no concrete detail available, the skill flags it rather than inventing one.

### 4. Cut filler, keep meaning
Every word must do work. If a sentence says the same thing without an adjective, the adjective was filler. If a paragraph says the same thing in two sentences, one of them is redundant.

### 5. Vary structure
Alternate between short and medium sentences. Start sentences with different words. Break the AI rhythm of subject-verb-object repeating endlessly.

### 6. Preserve the author's intent
The skill changes how something is said, not what is said. The core message, claims, and structure of the argument stay intact. Tone adjustments match the original context -- a marketing page stays persuasive, a technical doc stays precise.

---

## How the English and German Systems Differ

The skill handles both languages, but with distinct blacklists and pattern awareness.

- **German** has additional checks for compound noun abuse (Komposita-Monster) and the formal "Sie" constructions that AI overuses.
- **German** blacklists include words like "massgeschneidert", "ganzheitlich", and "Mehrwert" that are specific to German corporate AI writing.
- **English** blacklists focus on words like "delve", "landscape", "leverage", and "robust" that dominate English AI output.
- The **structural checks** (em-dashes, list length, passive voice, sentence openers) apply equally to both languages.

The skill detects which language the input text is written in and applies the appropriate blacklist automatically.

---

## Next Steps

- **Install the skill:** [INSTALLATION.md](INSTALLATION.md)
- **See usage examples:** [README.md](README.md)
- **Edit the skill:** The `skill.md` file is plain Markdown. Add your own banned words, adjust scoring thresholds, or add new checklist items to fit your writing style.
