# Lern My Speak (ver 1.0.0 beta)

<p align="center">
  <img src="./assets/clod-slackers.svg" width="380" height="345" alt="Two tall, slouching cartoon teenagers smirking and mumbling, with tiny orange-headed Clod standing between their feet, looking up.">
</p>

**A toy skill and a shorthand skill, at once** — [← back to Clod Code Agentic Skills](../README.md)

One person's own personal jargon, defined once so an assistant stops guessing at it from context and just reads it correctly instead. The complete operating definition is in [`SKILL.md`](./SKILL.md).

## Toy skill and shorthand skill, at once

This is comical to read — a glossary of someone's own casual typing shorthand looks funny laid out as a formal table. It's also a genuinely small, real utility: a long session develops its own vocabulary, and re-explaining or re-inferring the same handful of words every time is friction worth removing. There's a second kind of friction this happens to help with too: QWERTY layouts make certain words — "probably" is a common one — more typo-prone for an unskilled typist, and a short, clearly-defined stand-in like "prolly" sidesteps that risk entirely. Both labels are accurate at once; neither cancels the other out.

## Where this came from

This grew out of a real, specific constraint, not an invented quirk. This project's own author has had reduced finger mobility since the teens, making full, precisely-spelled typing more effortful and more error-prone than it is for most people. Leaning on short, phonetic shorthand instead of typing every word out in full is a genuine adaptation to that, not casual laziness — the same root cause behind the typo-proneness mentioned above, generalized past just one example.

## How it works

Say the phrase "lern my speak" — wrapped in whatever sentence feels natural, or on its own — and it's active for the rest of the session. No need to repeat it on every message afterward.

Once active, every term in the glossary gets read as its listed meaning, not guessed at or asked about.

## Make it your own

The glossary — kept short specifically so it's easy to hand-edit, in [`SKILL.md`](./SKILL.md) — is one person's real shorthand:

- **birth / rebirth** — new session
- **bish** — target, the thing being worked on or referred to (not the word it resembles) — "commie dis bish" = "commit this target"
- **booldung** — bull excrement (not literally, something taken as not likely)
- **Clod / Gem / Cop / Korg / Chad** — Claude / Gemini / Copilot / Grok / ChatGPT
- **commie** — commit (and push — always push too)
- **da** — do
- **dis / dat** — this / that
- **fer** — for
- **flock** — infers you know what
- **flying flock** — infers frustration over subject or context
- **gots** — got, have
- **ino** — i know
- **lemme ax** — let me ask
- **lez do [dis]** — let's do [this]
- **prollem** — problem
- **prolly** — probably
- **splain** — explain
- **stinking / im stinking** — thinking / I'm thinking
- **thot** — thought
- **toll** — told
- **wid** — with
- **wud** — what

Add, remove, or redefine entries to match your own. There's no live "define X as Y" mechanism mid-session — growing the list means opening the file and adding a line, the same way every other skill in this repo gets maintained.

**One warning, not a guardrail:** map a term to another installed skill's trigger phrase, or to a destructive action, at your own risk. This skill has no technical check against that collision — whoever edits or uses the list as is, owns the consequences.

## Related skills

- [Autonomon](../autonomon) — the other skill here that shapes ongoing AI behavior rather than a one-shot action, in the opposite direction: autonomon is always-on with no keyword at all and shapes the assistant's own output, this one needs one explicit trigger per session and shapes how your input gets read.
- [Don't Pollute Comments](../dont-pollute-comments) — the other skill built explicitly as a starting template to hand-edit into your own house style, triggered by name as a deliberate courtesy rather than running autonomously.

## Disclaimer

Use these skills at your own risk. The repository owner provides them "as is," without warranties, and is not liable for any loss, damage, claim, or consequence arising from their use, to the fullest extent permitted by law. You are responsible for reviewing outputs, commands, files, and results before relying on them.

---
[← back to Clod Code Agentic Skills](../README.md)
