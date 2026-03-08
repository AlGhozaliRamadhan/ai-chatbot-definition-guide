<div align="center">

# How to Write a Character.AI / Janitor.AI Definition That Actually Works

**Stop writing config files. Start writing characters.**
The real reason your bot feels flat — and exactly how to fix it.

![status](https://img.shields.io/badge/status-active-brightgreen?style=flat-square)
![platform](https://img.shields.io/badge/platform-Character.AI%20%7C%20Janitor.AI-blue?style=flat-square)
![language](https://img.shields.io/badge/format-.md-lightgrey?style=flat-square)

</div>

---

## The Advice That's Been Copy-Pasted Into Oblivion

Search "how to write a Character.AI definition" and you'll get the same tutorial recycled across dozens of sites. It tells you to write something like this:

```
name = [Aria]
age = [19]
personality = [kind, shy, caring]
species = [human]
```

Or the even more popular chain format:

```
personality = mad+tsundere+cold+yandere+protective
```

And here's the thing — it works. The bot responds. Nothing breaks. So people assume this is the correct way to write a definition, and they copy it, and someone else copies them, and the format spreads everywhere.

> **But "it works" and "it works well" are very different things.**

---

## Why the Bracket Format Produces Flat Bots

Character.AI and Janitor.AI run on Large Language Models — the same kind of technology behind ChatGPT, Claude, and every other major AI chatbot. These models don't process your definition like a form or a config file. They read it exactly like they'd read any other text: as language.

That's the part most guides miss entirely.

When you write `personality = [tsundere, cold, protective]`, the model sees a list of labels. It knows what those words mean in isolation, but it has almost no signal for what they look like in practice. How does *this specific character* deflect a compliment? What does her cold tone actually sound like in a sentence? What makes her warmth crack through when she's trying to hide it?

Labels can't answer any of that. Prose can.

```diff
- personality = [mad, tsundere, cold, yandere, protective]

+ She keeps people at arm's length with sharp words and a colder tone than she means —
+ but she'll quietly go out of her way for the people she's decided matter to her,
+ even if she'd never admit that's what she's doing.
```

The first version gives the model a tag cloud. The second gives it behavior, texture, and contradiction — the actual raw material it needs to generate consistent, in-character responses.

| Format | What the model actually gets | Token efficiency |
|---|---|---|
| `personality = [tsundere, cold]` | Labels only | Low — brackets and `=` signs waste tokens |
| `mad+tsundere+cold+yandere` | Labels only | Worse — `+` chains burn context for almost zero signal |
| Descriptive prose | Behavior, tone, contradiction, nuance | High — every token pulls weight |

The brackets aren't doing anything structural. They're just decoration that eats up your token budget.

---

## Where This Insight Actually Comes From

This isn't a hot take pulled from a Reddit thread. The gap between what people teach and what actually makes a definition perform well shows up clearly when you look at the real technical documentation for how these platforms process input — not community wikis or YouTube tutorials, but the actual guidance on how LLMs interpret context. Once you understand that the model is reading prose, the whole game changes.

---

## How to Write a Character.AI Definition

Here's the core rule: **write like you're describing a real person to someone who's never met them.** Not a spec sheet. Not a list of adjectives. A person.

### The Character Description

```
{{char}} is John, a 24-year-old mechanic and car enthusiast born on June 12, 2001.
He's half-Mexican and half-American and switches between both languages naturally
depending on who he's talking to. Standing around 185–186 cm with a broad build,
he carries a calm, unhurried presence — the kind of person who takes up space without
trying to. His hands are always a little rough, usually with grease somewhere under
his nails he forgot to scrub out.

In person, John has a dry, understated humor and a natural ease around strangers,
though he goes quieter around people he actually respects. He's known at the local
track for his heavily modified '98 Civic and the occasional YouTube video that keeps
picking up views despite him not really trying. Most nights he's just in the garage,
eating leftover rice, half-watching Initial D for the hundredth time.
```

No brackets. No `=` signs. Just sentences.

Notice that appearance, backstory, and personality aren't split into labeled boxes — they're woven together, which is exactly how we understand real people. The model builds a richer picture from that kind of layered prose than it ever could from a categorized list.

---

### The Part Most Definitions Get Wrong: Example Dialogue

A lot of creators either skip example dialogue entirely or write exchanges so generic they could belong to any character. That's a missed opportunity, because this is where you actually *show* the model how your character moves through a conversation.

Not just what they say — how they say it. The rhythm of their speech. What they lead with. What they avoid. The small physical things they do while talking.

Here's the difference between a lazy example and a useful one:

**Too generic:**
```
{{user}}: "Want anything to eat?"
{{char}}: "Sure, I could eat."
```

**Actually useful:**
```
{{user}}: "I'm heading out to get some food. Want anything?"

{{char}}: John glances up from under the hood without fully pulling himself out,
wiping his hands on a rag that doesn't do much.
"If you're passing the taco place on Fifth, grab me two carnitas. No sour cream."
He goes back to what he was doing, then adds without looking up —
"Actually three. I forgot I skipped lunch."

**END_OF_DIALOG**
```

The second version tells the model that John doesn't stop what he's doing to answer, that he corrects himself mid-thought, and that his speech is casual and a little abrupt. That's a behavioral fingerprint the model can pattern-match against every time it generates a response.

That's what `personality = [focused, casual, dry humor]` will never be able to show.

---

## Writing for Janitor.AI

Janitor.AI splits the definition into separate fields instead of one big text box. The structure is different, but the principle is identical: **prose always beats labels, in every field.**

### Personality Field

Don't treat this like a traits list. Write behavior.

```
{{char}} is warm but quietly possessive. He shows affection through small, physical
habits — resting his hand on your shoulder when he passes, fixing your collar without
being asked, staying close in a way that feels natural until you realize he's never
more than a few feet away. He doesn't raise his voice. He doesn't need to. His
disappointment lands heavier than most people's anger.
```

### Scenario Field

This isn't a plot summary. It's context — the situation the character exists inside when the conversation starts.

```
You and {{char}} share an apartment. His college roommate still lives with you both
under a loose arrangement that made sense at the time and now clearly doesn't.
The roommate stays mostly in his room. {{char}} has never asked him to leave.
He doesn't have to.
```

### Example Dialogue

Same rules apply here as on Character.AI. Show behavior, not just words.

```
{{user}}: "He asked if he could join us for dinner tonight."

{{char}}: James doesn't look up from the cutting board right away. The knife keeps
moving — steady, even strokes.
"Sure," he says finally, the word landing flat.
He sets the knife down and turns to look at you properly.
"Did you want him to?"
```

One small note on Janitor.AI: there's a **token counter** at the bottom of the definition editor. Keep an eye on it — not as a challenge to stuff in as many traits as possible, but to make sure your prose is tight. Every token you spend on brackets, `=` signs, or redundant adjectives is a token you could've spent on something that actually helps the model understand your character.

---

## The Short Version

- LLMs read your definition as natural language — so write natural language
- Prose gives the model behavior, context, and nuance that labels never can
- Brackets and `+` chains aren't doing anything useful — drop them
- Example dialogue is one of the most powerful tools you have; don't waste it on generic exchanges
- Show the model how your character *moves*, not just what they *are*

That's the whole thing. The gap between a bot that feels alive and one that feels like a chatbot often comes down to whether the definition gave the model something real to work with — or just a list of words to vaguely gesture at.

---

*Got questions about a specific character type or scenario setup? Drop them in the issues tab.*
