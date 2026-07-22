# eat

A Claude Code skill for **knowledge extraction** — pull the frameworks, methods, numbers,
and non-obvious insights out of any source without reading/watching the whole thing.

Invoke with `/eat <url-or-file>` (or "eat this", "eat from …").

## What it handles

| Source | Method |
|--------|--------|
| YouTube | yt-dlp subtitles → Groq audio → local Whisper fallback |
| Instagram / TikTok / X video | yt-dlp (cookie-auth) → Whisper → frame extraction |
| Podcast / direct audio | yt-dlp download → Groq / Whisper transcription |
| X/Twitter thread | free syndication API → browser → paid X API (last resort) |
| Web article | defuddle (clean markdown) → WebFetch fallback |
| Local file / PDF | Read directly |

Output always starts with **Source:** [title] — [URL], then knowledge organized by
category (mental models, methods, techniques, key numbers, contrarian insights, etc.).
Depth scales to insight *density*, not raw length.

## Install

Copy this directory into your Claude skills folder as `eat/`
(e.g. `~/.claude/skills/eat/`), then invoke with `/eat`.

## Dependencies

**Required:** `yt-dlp`, `ffmpeg`.
**Transcription (one of):** `whisper` (local, free) or `GROQ_API_KEY` (cloud, faster).
**Optional:** `defuddle` (cleaner article extraction), `X_BEARER_TOKEN` (paid X API, last resort).

No secrets are stored in this repo — the scripts read `GROQ_API_KEY` / `X_BEARER_TOKEN`
from the environment. See `SKILL.md` for full setup, including one-time browser-cookie
export for authenticated social-media downloads.

## License

MIT © catcatcat
