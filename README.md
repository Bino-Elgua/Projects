# 🔮 Vanity-Eth-Pro — ÀṣẹMirror Base Edition

**The unified shrine for Technosis** — A foundational AI-powered knowledge management platform for indexing, searching, and visualizing the Technosis ecosystem (oso-lang, osovm, techgnosis, ifascript).

This is the **base edition** of ÀṣẹMirror — a streamlined starting point with configuration UI, visualization components, and authenticated API access.

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🔍 **Semantic Search** | RAG-powered search across 4 GitHub repos via Qdrant |
| 🏛️ **7-Layer Pyramid** | Visual Technosis stack (Genesis → Shrines) |
| 📅 **Timeline** | 7-year inheritance lock countdown + 90-day phases |
| 💰 **1440 Wallet Tree** | Soul-bound inheritance derivation tree |
| 🎁 **Tithe Flow** | 50/25/15/10 split visualization |
| ⚙️ **Settings Modal** | Multi-LLM provider selection (6 providers) |
| 🔑 **Auth API** | Bearer token authentication via `phoneKey` |
| 🌑 **Dark Theme** | Black/red/ash sacred palette (Tailwind) |

---

## 🚀 Quick Start

### 1. Install
```bash
cd vanity-eth-pro
npm install
```

### 2. Configure Environment
```bash
cp .env.example .env
```

Edit `.env` with your preferred LLM provider:
```env
LLM_PROVIDER=openai
OPENAI_API_KEY=sk-...
QDRANT_URL=http://localhost:6333
```

Supported providers: `openai` | `claude` | `gemini` | `mistral` | `groq` | `cohere`

### 3. Start Qdrant (optional)
```bash
docker run -d --name qdrant -p 6333:6333 qdrant/qdrant
```

### 4. Index Repos
```bash
npm run index
```

Syncs 4 GitHub repos → chunks code → creates embeddings → uploads to Qdrant.

### 5. Run Dev Server
```bash
npm run dev
```

Visit: **http://localhost:1111**

---

## 📁 Project Structure

```
vanity-eth-pro/
├── src/
│   ├── App.svelte              # Main app — config view + next steps
│   ├── main.ts                 # Entry point
│   ├── app.css                 # Global styles
│   ├── components/
│   │   ├── Pyramid.svelte      # 7-layer stack visualization
│   │   ├── Timeline.svelte     # 7-year countdown + phases
│   │   ├── WalletTree.svelte   # 1440 inheritance tree
│   │   ├── TitheFlow.svelte    # Tithe split diagram
│   │   ├── Settings.svelte     # LLM provider config modal
│   │   └── SearchBar.svelte    # Search input component
│   ├── lib/
│   │   ├── api.ts              # API client with Bearer auth (phoneKey)
│   │   ├── store.ts            # Svelte stores
│   │   └── test.utils.ts       # Test utilities
│   └── routes/
│       └── api/+server.ts      # Backend API endpoints
├── indexer.ts                  # GitHub → chunk → embed → Qdrant pipeline
├── llm-sdk.ts                  # Multi-provider LLM abstraction (6 providers)
├── api.ts                      # Backend route stubs
├── AIcouncil/                  # AI council module
├── dist/                       # Production build output
├── index.html                  # SPA entry
├── vite.config.ts              # Vite config
├── tailwind.config.js          # Tailwind CSS
├── Dockerfile                  # Container build
├── vercel.json                 # Vercel deploy config
└── wrangler.toml               # Cloudflare Workers config
```

---

## 🔌 API Client

The API client uses Bearer token auth via `phoneKey`:

```typescript
import { search, chat, getTimeline, visualize } from '$lib/api';

// Semantic search
const results = await search("Where does @guardian live", phoneKey);

// Multi-turn chat
const response = await chat(messages, phoneKey);

// Timeline data
const timeline = await getTimeline(phoneKey);

// Visualizations
const pyramid = await visualize("pyramid", phoneKey);
```

All calls go to `POST /api` with `Authorization: Bearer <phoneKey>` header.

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Svelte 4 + Tailwind CSS 3 |
| Bundler | Vite 5 |
| Vector DB | Qdrant (cosine similarity) |
| LLM | 6 providers via `llm-sdk.ts` |
| Indexer | TypeScript (tsx) + GitHub API |
| Auth | Bearer token (phoneKey) |
| Deploy | Vercel / Cloudflare / Docker |

---

## 🚢 Deployment

### Vercel
```bash
vercel
```

### Cloudflare
```bash
npm run build && wrangler deploy
```

### Docker
```bash
docker build -t vanity-eth-pro .
docker run -p 1111:1111 --env-file .env vanity-eth-pro
```

---

## 🔑 Key Differences from Evil-Twin

Vanity-eth-pro is the **base edition**:
- Streamlined `App.svelte` — config status + next steps (no tabbed navigation)
- API client uses Bearer token auth (`phoneKey` parameter)
- No `ChatBox.svelte` — chat handled at API level
- Plain JavaScript Svelte (`<script>` not `<script lang="ts">`)
- Tailwind utility classes inline (vs custom CSS in Evil-twin)

---

## 📜 Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start Vite dev server |
| `npm run build` | Production build to `dist/` |
| `npm run preview` | Preview built version |
| `npm run index` | Index all 4 repos into Qdrant |
| `npm run search` | CLI search tool |

---

## License

Built for Technosis. Àṣẹ. 🤍⚡🍶
