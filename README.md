# AI Field Map

An interactive wall chart of the field of artificial intelligence, in a single HTML file. It shows how the fields of study nest inside each other, how they connect, and which models and products come out of them. It also includes guided learning paths and a reading list where you can track your progress.

**Live site:** https://zulfanahmadi12.github.io/AI-Study-Path/

Or open `index.html` locally in any modern browser. There is no build step, no server and no install.

## What's on the map

The map is a stack of colour-coded layers. Each layer opens up one item from the layer above it:

| Layer | What it covers |
|---|---|
| **Artificial Intelligence** | The seven core abilities: reasoning, learning, perception, language, action, memory, and responsible and safe AI |
| **Subfields of AI** | Symbolic AI, search and planning, NLP, computer vision, speech, ML, deep learning, robotics, multi-agent systems, AI safety |
| **Machine Learning** | Learning paradigms, problem types, algorithms, optimization, evaluation, ML systems |
| **Deep Learning** | Core concepts, architectures (Transformers, CNNs, RNNs, diffusion…), training techniques, capabilities, applications |
| **Foundation Models** | Characteristics, training objectives, modalities, adaptation methods (prompting, fine-tuning, RAG, alignment, tools) |
| **Model families** | Language, vision, multimodal, speech, generative and embedding models, with language models broken down further (autoregressive, masked, encoder-decoder, LLMs, instruction-tuned) |
| **What these fields produce** | Real **models** (GPT/Claude/Llama/Gemini, BERT, T5, CLIP, Stable Diffusion, Whisper, ResNet/YOLO, AlphaGo) and **products** (chat assistants, RAG search, agents, translation, self-driving cars, recommendation feeds, spam and fraud detection) |

A nested-box diagram at the top summarises the containment: AI ⊃ ML ⊃ DL ⊃ Foundation Models ⊃ LLMs.

## For newcomers

AI is a big field that moves fast, and it's hard to know where to start. The page is built around that:

- **A note before you start** at the top explains why the map exists and how to use it. It can be collapsed, and the page remembers your choice.
- **Where should I start?** asks what you want to do and what you already know, then suggests one learning path and a second one to follow it.
- **Pace labels** on each layer mark it *Stable*, *Slow-changing* or *Fast-moving*, so you can tell the slow-changing foundations from the news.
- **Keeping up** gives a few ways to follow new work without chasing every headline, with a short list of sources.
- **Where is this?** is for when you're reading something and get lost. Paste a paragraph, and the page finds every term it knows, groups them by layer, and tells you which part of AI the text is mostly about. Each term links to its place on the map.
- **Inline definitions:** jargon words on the map cards have a dotted underline. Tap one for a short definition, with links to the map and the glossary.

## How to use it

- **Select any ringed title or item** to see it in the side panel: a description, what it **builds on**, what it **leads to**, a **learning trail** of what sits further back (the fundamentals behind its ingredients), and what to read about it.
- **Wires** are drawn over the chart for the selected item:
  - *Solid line*: builds on (an ingredient of the selected item)
  - *Dashed line*: leads to (something it makes possible)
  - *Grey line*: opens up (a layer that expands an item from the layer above)
- **Search** in the side panel to find items on the map, in the reading list and in the glossary (e.g. `transformer`, `Whisper`, `Sutton`). Press **Enter** to jump to the first result.
- Use the **top bar** to jump between the map, learning paths, books and sources, keeping up, and the glossary. The current section is highlighted as you scroll.
- Press **Escape** to clear the search, or the current selection if there is no search.

### Learning paths

Six guided routes. Start one and the side panel walks you from stop to stop, with a source to read at each. The page remembers which steps you have visited, so a path card offers to continue where you left off, and the last step suggests where to go next:

| Path | Level |
|---|---|
| From zero to understanding GPT | Beginner |
| Practical machine learning on real data | Beginner |
| How image generators work | Intermediate |
| Building with LLMs | Intermediate |
| AI that plays and moves | Advanced |
| Self-improving agents | Advanced |

### Books and sources

About 94 curated sources (books, courses, papers, guides and videos), arranged in shelves by field. Each one is tagged with:

- **Type**: book, course, paper, guide or video
- **Cost**: free or paid
- **Level**: beginner, intermediate or advanced
- **Prerequisites**: none, Python, university maths, or an ML background
- **Time to finish**: a rough estimate in hours

You can filter by any of these and **tick sources off** as you finish them. A progress bar tracks how far you've got.

> Hours, prerequisites and levels are rough estimates, judged rather than looked up. Most links were checked on 2 October 2026.

### Glossary

About 174 AI terms in plain language, including newer agent and LLM vocabulary such as *agent harness*, *context engineering*, *KV cache* and *mixture of experts*, from *accuracy* to *zero-shot*. Each entry gives a short definition, other names the term goes by, and a link to its place on the map.

- **Filter** the list by typing, or **jump to a letter**.
- The **side panel search** finds glossary terms too.
- **Selecting a map item** lists its glossary terms in the side panel.
- A search with no match suggests the closest topics instead of stopping at "No matches".

## Saving progress

- Finished ticks, filter choices, visited path steps, your answers to *Where should I start?* and whether the welcome note is open are saved in your browser's `localStorage` (`aimap.done`, `aimap.filters`, `aimap.steps`, `aimap.choose`, `aimap.note`).
- When the page is opened as a Claude artifact with database and user access, ticks also sync to your Claude account, so they follow you across devices. The line above the progress bar shows which storage is in use.

## Under the hood

- **Single self-contained file**: HTML, CSS and vanilla JavaScript, with no dependencies. The only external request is Google Fonts (Inter), and the page falls back to system fonts without it.
- **Visual design**: a calm productivity style with a blue top navigation bar, quiet neutral working surfaces, Inter type and a three-blue accent hierarchy. Each layer of the map keeps its own accent colour.
- **Light and dark themes** follow your system setting by default. The theme button in the top bar cycles System → Light → Dark and remembers your choice (`aimap.theme`).
- **Responsive**: wires are redrawn on resize, and the layout works down to phone width.
- **Content lives in plain data structures** near the top of the `<script>`, so you can edit it without touching the rendering code:

| Variable | Contents |
|---|---|
| `BANDS` | The layers, cards and items on the map |
| `LINKS` | Connections between nodes: `[from, to, label]` |
| `LIB` | Sources: `key: [type, title, author, note, url, free]` |
| `PAID`, `LEVEL`, `META` | Cost, level, and `[prerequisite, hours]` for each source |
| `READS` | Which sources to show for each map node |
| `SHELF` | How the reading list is grouped |
| `PATHS` | The learning paths and their steps |
| `NEXT` | Which paths to suggest after finishing each one |
| `PACE` | The pace label and note for each layer |
| `FOLLOW` | Sources listed under Keeping up |
| `GLOSS` | Glossary entries: `[term, other names, definition, map node id]` |

To add a connection, append to `LINKS` using existing node ids. Links that point to unknown ids are dropped, with a warning in the console.
