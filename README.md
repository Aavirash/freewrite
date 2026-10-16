# freewrite — an on-device AI companion fork

A distraction-free macOS app for **freewriting** and **video journaling** — and now, a quiet
on-device AI writing companion that lives *inside* the text, never on top of it.

> This is a **fork of [`farzaa/freewrite`](https://github.com/farzaa/freewrite)** by
> **[Farza Majeed](https://x.com/farzatv)**. The original app, its design, and its philosophy
> are his. This fork keeps everything he built and adds a set of features on top. Full credit
> and thanks below.

---

## What is freewrite?

Freewriting is a writing technique from 1973: write continuously for a set time without
worrying about grammar, spelling, or editing — a pure stream of consciousness. freewrite is a
minimal macOS app built around exactly that. You open it and write. No "new document", no
formatting, no toolbar clutter — just you and the words, with a timer and an optional
no-backspace rule to keep you moving forward.

It also records **video entries** (with on-device transcription), keeps everything as plain
markdown in `~/Documents/Freewrite/`, and never sends your writing anywhere.

---

## What this fork adds

### Ghost companion — on-device Apple Intelligence
Press **⌘G** and an AI companion starts *watching*. When you pause, it reads your writing up to
the caret and streams a short, supportive thought **inline as dimmed "ghost" text past your
cursor** — never in a popup, never stealing the caret.

- The caret jumps to the end of the note, which ends with `↵  ask about this…`.
- Type your question right there and press **Return** to send it.
- Your question clears, the caret returns to where you were writing, a spinner appears, and the
  answer streams back **as ghost at the cursor** — even if you kept typing.
- **Backspace** dismisses a suggestion and stops the companion until you press ⌘G again.

It runs on **Apple's on-device Foundation Model** via the Foundation Models framework. No API
keys, no network, no accounts. Your writing stays on your Mac. Requires **macOS 26+ with Apple
Intelligence enabled** (the companion is simply unavailable on older systems).

### Keyboard shortcuts
| Shortcut | Action |
|---|---|
| ⌘G | Arm / disarm the ghost companion |
| ⌘N | New entry |
| ⌘B | Toggle backspace on/off |
| ⌘F | Toggle fullscreen |
| ⌘R | Randomize font |
| ⌘T | Start / pause the timer |
| ⌘O | Record a video entry |
| ⌘Y | History sidebar |
| `` ` `` / `~` | Toggle light / dark theme |

### Editor & feel
- **Top / center alignment toggle** — on tall screens, start your writing from the top or
  from a little above the middle. Remembered across launches.
- A custom `NSTextView`-based editor that keeps the caret aligned with the line, with a soft
  **white glowing caret** and a matching glowing ring spinner while the companion is thinking.
- Smart quotes, autocorrect and spellcheck are off — on purpose.

### Build & tooling
- **GitHub Actions CI** builds the `.app` on every push to `main` (macOS 26 / Xcode 26 runner)
  and uploads it as a downloadable artifact — no local Xcode required to get a build.

---

## Requirements

- **macOS 14+** for the base app.
- **macOS 26+ with Apple Intelligence** for the ghost companion. On older systems everything
  else works; the companion is just disabled.

## Build

**Locally** (needs Xcode):

```bash
xcodebuild -project freewrite.xcodeproj -scheme freewrite -configuration Release build
```

**Without Xcode** (uses this repo's CI):

```bash
gh workflow run build.yml
gh run download --name freewrite-app   # then unzip and open freewrite.app
```

---

## Where your writing lives

Everything is local, plain files under `~/Documents/Freewrite/`:

- `[UUID]-[date].md` — text entries
- `Videos/[UUID]-[date]/` — video entries: the `.mov`, a `thumbnail.jpg`, and a `transcript.md`

No analytics. No servers. Nothing leaves your machine.

---

## Credits

- **Original app, design and idea: [Farza Majeed](https://x.com/farzatv)** —
  [`farzaa/freewrite`](https://github.com/farzaa/freewrite). This project simply would not exist
  without his work, and the whole philosophy here is his.
- **This fork: [Aavirash](https://github.com/Aavirash)** — added the on-device ghost companion,
  keyboard shortcuts, alignment toggle, and the CI build.

If you build something on top of freewrite, please keep giving Farza credit.

## License

MIT — see [LICENSE](LICENSE). Original copyright © 2025 Farza Majeed.
