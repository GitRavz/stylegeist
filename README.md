<h1 align="center">✨ stylegeist</h1>
<p align="center"><em>The zeitgeist of my design systems.</em></p>
<p align="center">A personal library of reusable UI design specs — colors, tokens, layouts, and component recipes — written in Markdown so they can be dropped into any project or handed to any AI/dev to recreate the look.</p>

---

## 📚 Systems

| System | Vibe | Spec |
|--------|------|------|
| **Ink & Paper** | Print-shop UI — near-black *ink* sidebar, white *paper* cards, CMYK accents | [`ink-and-paper/`](ink-and-paper/README.md) |

<!-- Add a new row above for each system you drop in. -->

---

## 🗂️ How this repo is organized

```
stylegeist/
├── README.md            ← you are here (the index)
├── ink-and-paper/
│   └── README.md        ← full portable design spec
└── <future-system>/
    └── README.md
```

**To add a new design system:** create a folder, drop a `README.md` spec inside it, then
add a row to the table above.

## 🚀 How to use a spec

Each spec is self-contained. Open the folder's `README.md` and:

1. Copy the **prompt preamble** to the top of your AI prompt (sets the overall direction).
2. Paste the **design tokens** block into your `:root {}`.
3. Follow the **layout shell** + **component recipes** to build screens.

---

<p align="center"><sub>Built and maintained by <a href="https://github.com/GitRavz">@GitRavz</a>.</sub></p>
