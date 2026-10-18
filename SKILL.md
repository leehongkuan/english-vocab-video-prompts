---
name: english-vocab-video-prompts
description: Write English prompts for short vocabulary teaching videos using “This is the …”, two seconds per vocabulary item, reference-image presenters or teacher Milo, and automatic batches of up to five items. Use for Google Flow or similar video prompt requests, including 英语词汇教学视频提示词.
---

# English Vocabulary Video Prompts

Produce ready-to-paste **English prompts**, not videos, for Google Flow by default or the video tool the user names. Surrounding explanations may use the user's language. Do not invoke video generation unless requested.

## Inputs and presenter

- Accept any nonempty ordered list of vocabulary items. A multiword phrase such as `concrete mixer` counts as **one item**. Preserve order and intentional duplicates; remove list numbering, not vocabulary. If no vocabulary is supplied, ask for it.
- Use the person in the uploaded character reference when supplied. Preserve their face, hair, clothing, and accessories across all shots and clips. Use the user's character name if given; otherwise call them “the presenter”, without guessing their real identity. Match voice direction to the supplied character description; otherwise use a warm, clear American English voice.
- Without a character image, default to **Milo, an adult male English teacher**, with a friendly expression, short dark hair, a light blue button-down shirt, dark trousers, and a warm, clear American male voice. Establish this description once and repeat it consistently in each clip. Explicit user character choices override this fallback.
- Reference only assets actually provided. For Flow, say “the provided character reference image”; do not invent asset IDs or import another platform's reference syntax. A user-provided audio reference controls voice consistency when available.

## Duration and batching — strict

Every vocabulary item gets **exactly 2 seconds**, including quiz and answer.

Split the ordered items into consecutive groups of at most five:

- 1–4 items: one clip lasting `item_count × 2` seconds.
- 5 items: one 10-second clip.
- More than 5: a 10-second clip per full group of five, then a separate `remainder × 2` second clip if there is a remainder.
- Never create an empty remainder clip. Examples: 6 → 10+2 seconds; 8 → 10+6; 10 → 10+10; 13 → 10+10+6.
- Explicit user grouping overrides the default (for example, eight items in two 8-second clips).
- **Ask before proposing to implement any duration change.** Do not silently slow down long words, pad a remainder, repeat items to fill time, or convert a 2-second item into a longer one.
- These are requested prompt timings, not claims about a platform's supported export lengths. If an actual generation tool rejects a duration, explain the constraint and ask how to handle it before changing timing. Prompt-writing alone does not require checking current platform specs.

## Teaching format

For item index `i` within a clip (starting at zero), its shot starts at `s = 2 × i`:

1. `s` to `s + 0.5`: silent quiz. Show `This is the ____.` with one blank per whitespace-separated word in the item. The presenter already points at the target.
2. `s + 0.5` to `s + 2`: reveal `This is the <item>.` and say this complete sentence **exactly once**. Highlight only the target word or whole phrase in yellow.
3. After speaking, close the mouth and hold the pose until the cut. No extra reading, repeated sentences, isolated word repetitions, explanations, greetings, or closing remarks.

Use natural lowercase common nouns in the sentence, preserving proper noun spelling. Keep the requested “This is the …” structure. If an item cannot fit it grammatically (for example a plural noun or an action verb), ask one targeted question about the intended noun or sentence rather than silently changing vocabulary or teaching an incorrect construction.

## Visual and audio direction

- Default to photorealistic 9:16 vertical video, clear natural light, and one static shot per item. Hard-cut exactly at 2-second boundaries. No pans, zooms, tracking, or animated transitions.
- Choose a coherent setting appropriate to the vocabulary, not a fixed car or construction setting for every topic.
- Start each shot with the presenter already positioned and pointing. Keep their face and the target visible together where practical. Sync visible lip movement to speech.
- Describe concrete identifying features and point precisely to the named object or part. Distinguish easily confused items, such as wheel/tire/rim or bulldozer/loader. Do not invent a vehicle part or unsupported brand detail to fit the example.
- Keep machinery parked and demonstrations simple. Do not spend the two seconds on walking, opening compartments, or complex operations.
- Warm, clear American English speech, compact enough to finish the sentence within its 1.5-second answer window. No background music, other voices, sound effects, or machine noise by default.
- Only the specified English teaching subtitles: large sans-serif type, lower safe area, white text with dark outline. Answer term: yellow background with dark letters. Stable placement, correct spelling, no Chinese text, phonetics, titles, or numbering. Keep multiword target phrases together when wrapping.

## Output

Give a short batching summary, followed by **one self-contained English prompt code block per clip**. Repeat the actual presenter description, environment, timing, speech, and subtitle rules inside each block so it works independently; do not require the user to prepend a shared template or refer to a previous clip.

Each prompt must include:

- Exact total duration and number of 2-second shots.
- Presenter/reference and voice consistency instructions.
- Setting, fixed-camera framing, and hard-cut timestamps.
- Exactly one timeline entry per item, with silent quiz interval, reveal interval, literal quiz subtitle, literal answer subtitle, highlighted term, and the one spoken sentence.
- A final instruction to finish the last sentence and end at the specified duration.

Timeline entry pattern (replace every placeholder):

```text
0.0–2.0 SECONDS — TRUCK
Static shot. [Presenter] stands beside a parked cargo truck with its cab and cargo body clearly visible, already pointing toward it.
0.0–0.5: Silence. Quiz subtitle: “This is the ____.”
0.5–2.0: Replace with “This is the truck.” Highlight “truck”.
[Presenter] says exactly once: “This is the truck.”
Then close the mouth and hold the pose until the cut.
```

Before returning, check that every input item appears once in its original position, all intervals are contiguous, each shot is 2 seconds, each default clip has at most five items, total duration is twice the item count, and speech/subtitles/presenter instructions agree. Describe prompts as instructions for generation, not guarantees of exact model output.
