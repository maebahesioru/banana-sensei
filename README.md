# Banana Sensei 🍌🎓

**Know your banana. Use it right.**

Banana Sensei is a tiny browser app that looks at a photo of a banana and tells you how ripe it is — and what to make with it. Upload a photo, and a zero-shot image classifier (CLIP, running entirely in your browser) sorts it into:

- 🟢 **まだ青い** (unripe) → great for banana chips or cooking
- 🍌 **食べごろ** (ripe) → eat as-is, smoothies
- 🟤 **完熟** (overripe) → banana bread & cake time
- ⚠️ **そろそろ危ない** (spoiled) → toss it safely
- 🤔 **これは…バナナ？** (not a banana) → try again

Every verdict comes with advice from the "teacher" — what that ripeness is best for in the kitchen.

## Why

Bananas are the most-wasted fruit in many kitchens: people bin them exactly when they're at peak sweetness (brown!), or eat them green and chalky. A two-second check fixes that.

Made for **Banana Hacks 2026** (Image AI weekend hackathon, Oct 9–12).

## How it works

- **No server, no uploads.** The photo never leaves your device. Everything runs client-side.
- **Zero-shot classification** via [Transformers.js](https://github.com/huggingface/transformers.js) with the `Xenova/clip-vit-base-patch32` CLIP model (~90 MB, cached by the browser after first load).
- The model compares your photo against five text descriptions ("a photo of a green unripe banana", …) and returns confidence scores. No training data needed — that's the magic of CLIP.
- Single `index.html` — HTML, CSS and JS in one file. No build step.

## Run it

Open `index.html` in a browser, or:

```bash
python3 -m http.server 3961
```

First analysis downloads the model (progress is shown). After that it's instant.

## Files

- `index.html` — the whole app

## Notes

- Privacy: images are processed locally via `URL.createObjectURL`; nothing is sent anywhere.
- The "確信度" (confidence) meter shows how sure the teacher is. Small or cluttered photos may confuse it — fill the frame with the banana for best results.
