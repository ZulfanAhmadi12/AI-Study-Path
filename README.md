# AI Field Map

An interactive wall chart of the field of artificial intelligence, in a single HTML file. It shows how the fields of study nest inside each other, how they connect, and which models and products come out of them. It also includes guided learning paths and a reading list where you can track your progress.

Open `AI Field Map.html` in any modern browser. There is no build step, no server and no install.

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

## How to use it

- **Select any ringed title or item** to see it in the side panel: a description, what it **builds on**, what it **leads to**, and what to read about it.
- **Wires** are drawn over the chart for the selected item:
  - *Solid line*: builds on (an ingredient of the selected item)
  - *Dashed line*: leads to (something it makes possible)
  - *Grey line*: opens up (a layer that expands an item from the layer above)
- **Search** in the side panel to find items on the map and in the reading list (e.g. `transformer`, `Whisper`, `Sutton`). Press **Enter** to jump to the first result.
- Press **Escape** to clear the search, or the current selection if there is no search.

### Learning paths

Five guided routes. Start one and the side panel walks you from stop to stop, with a source to read at each:

| Path | Level |
|---|---|
| From zero to understanding GPT | Beginner |
| Practical machine learning on real data | Beginner |
| How image generators work | Intermediate |
| Building with LLMs | Intermediate |
| AI that plays and moves | Advanced |

### Books and sources

About 88 curated sources (books, courses, papers, guides and videos), arranged in shelves by field. Each one is tagged with:

- **Type**: book, course, paper, guide or video
- **Cost**: free or paid
- **Level**: beginner, intermediate or advanced
- **Prerequisites**: none, Python, university maths, or an ML background
- **Time to finish**: a rough estimate in hours

You can filter by any of these and **tick sources off** as you finish them. A progress bar tracks how far you've got.

> Hours, prerequisites and levels are rough estimates, judged rather than looked up. Most links were checked on 2 October 2026.

## Saving progress

- Finished ticks and filter choices are saved in your browser's `localStorage` (`aimap.done`, `aimap.filters`).
- When the page is opened as a Claude artifact with database and user access, ticks also sync to your Claude account, so they follow you across devices. The line above the progress bar shows which storage is in use.

## Under the hood

- **Single self-contained file**: HTML, CSS and vanilla JavaScript, with no dependencies. The only external request is Google Fonts (Archivo, Atkinson Hyperlegible, IBM Plex Mono), and the page falls back to system fonts without it.
- **Light and dark themes** follow your system setting.
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

To add a connection, append to `LINKS` using existing node ids. Links that point to unknown ids are dropped, with a warning in the console.
