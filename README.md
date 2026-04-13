# WABro 🤖

**WhatsApp Bot dengan AI Integration.**

Bot WhatsApp otomatis berbasis AI yang terintegrasi dengan LLM (Gemini, Groq, Ollama), dashboard web untuk kontrol, dan RAG knowledge base untuk jawaban berbasis pengetahuan.

## 🚀 Quick Start

```bash
# Install dependencies
pip install -r requirements.txt

# Install Playwright browsers
playwright install chromium

# Run dashboard (port 8899)
python dashboard_app.py

# Or run WhatsApp bot directly
python main.py

# Or use the auto-start script
./wabro.sh  # Auto-venv, port cleanup, dashboard start
```

---

## 📊 Dashboard

Access at: **http://127.0.0.1:8899**

Features:
- Start/Stop WhatsApp bot
- Switch LLM provider (Gemini/Groq/Ollama)
- View real-time logs
- Chat statistics & charts
- API keys management
- RAG knowledge base management

---

## 🔧 Configuration

### Dashboard Port

Edit `.env` to change dashboard port:

```bash
DASHBOARD_PORT=8899  # Change to any available port
```

## 📁 Project Structure

```
WABro/
├── docs/                       # Documentation
│   ├── architecture/           # Architecture docs
│   ├── modules/                # Module reference
│   ├── decisions/              # Architectural Decision Records
│   ├── FEATURES.txt            # Complete feature list
│   ├── TODO.md                 # Roadmap
│   └── TROUBLESHOOT.txt        # Troubleshooting guide
│
├── channels/whatsapp/          # WhatsApp Bot engine
│   ├── agents/                 # AI agents (ReAct pattern)
│   ├── adapters/               # LLM & WhatsApp adapters
│   │   ├── llm/                # LLM providers
│   │   │   ├── gemini.py       # Gemini API client
│   │   │   ├── groq.py         # Groq API client
│   │   │   └── ollama.py       # Ollama client (offline)
│   │   └── whatsapp/           # WhatsApp Web client
│   ├── services/               # Business logic
│   ├── rules/                  # Message rules engine
│   ├── skills/                 # RAG knowledge base
│   ├── monitoring/             # Error monitoring
│   └── logging/                # Chat logging
│
├── dashboard/                  # Web Dashboard (FastAPI)
│   ├── app.py                  # FastAPI application
│   ├── routes/                 # API routes
│   ├── templates/              # HTML templates
│   ├── static/                 # CSS/JS assets
│   └── state.py                # Runtime state
│
├── shared/                     # Foundation (base classes)
│   ├── bases.py                # BaseAgent, BaseService, BaseTool
│   ├── utils.py                # Decorators & utilities
│   ├── errors.py               # Custom exceptions (12 types)
│   └── services.py             # Shared services
│
├── config/                     # Configuration
│   ├── keys/                   # API keys (gitignored)
│   ├── ai_wa.py                # LLM configuration
│   └── prompt_common.txt       # System prompts
│
├── knowledge/                  # RAG Vector DB
│   ├── documents/              # Uploaded files
│   ├── web/                    # Crawled websites
│   └── vector_db/              # ChromaDB storage
│
├── reports/                    # Runtime Data
│   ├── agent/                  # Chat logs, stats
│   └── logs/                   # System logs
│
├── main.py                     # Main entry point (WhatsApp Bot)
├── dashboard_app.py            # Dashboard entry point
├── requirements.txt            # Python dependencies
└── wa_profile/                 # WhatsApp session (gitignored)
```

---

## 📖 Documentation

### **Core Documentation**

| File | Description |
|------|-------------|
| [`docs/architecture/architecture.md`](docs/architecture/architecture.md) | 🏗️ **System architecture overview** |
| [`docs/modules/modules.md`](docs/modules/modules.md) | 📦 **Complete module reference** |
| [`AI_INSTRUCTION.md`](AI_INSTRUCTION.md) | 📘 **Complete development guide** |
| [`docs/FEATURES.txt`](docs/FEATURES.txt) | Complete feature list |
| [`docs/TODO.md`](docs/TODO.md) | Roadmap & planned features |
| [`docs/TROUBLESHOOT.txt`](docs/TROUBLESHOOT.txt) | Troubleshooting guide |

### **Additional Resources**

| File | Description |
|------|-------------|
| [`config/ai_wa.py`](config/ai_wa.py) | LLM configuration (Gemini/Groq/Ollama) |
| [`config/rules-policy.txt`](config/rules-policy.txt) | AI response rules & policies |

> **💡 Tip:** For development work, start with [`docs/architecture/architecture.md`](docs/architecture/architecture.md) for big picture, then [`docs/modules/modules.md`](docs/modules/modules.md) for module details.

---

## 🎯 Key Features

### **WhatsApp Bot Automation**
- ✅ **WhatsApp Web Automation** - Playwright-based automation
- ✅ **Group Support** - Mention/reply detection only (no spam) - **STRICT ENFORCED**
- ✅ **Private Chat** - Full response mode
- ✅ **Message Deduplication** - Hash-based duplicate detection
- ✅ **Message Age Filtering** - Ignores messages older than 1 hour
- ✅ **Multi-line Message Sending** - Clipboard paste (avoids WhatsApp splitting)
- ✅ **Reply Chaining** - Quotes original message in replies
- ✅ **Quote/Reply Detection** - Multiple DOM selectors for accurate detection
- ✅ **Automatic Reconnection** - Retry logic with exponential backoff
- ✅ **Popup/Dialog Handling** - Auto-dismisses "Link this device" prompts
- ✅ **Chat Type Detection** - High-accuracy multi-priority algorithm

### **AI Integration**
- ✅ **Multi-LLM Support** - Gemini, Groq (4 models), Ollama (offline)
- ✅ **Groq 4-Tier Model Routing** - Auto-routes by complexity (greeting→8B, general→20B, factual→70B, coding→120B)
- ✅ **Smart Replies** - Context-aware responses
- ✅ **Rules Engine** - 13 hardcoded rules (bypasses LLM)
- ✅ **RAG Knowledge Base** - Document upload + web crawling (HYBRID/FULL RAG/GENERAL AI modes)
- ✅ **Guided Freedom** - Creative, varied responses (temperature 0.8, no templates)
- ✅ **API Key Rotation** - Round-robin with persistent index (survives restarts)
- ✅ **Web Search** - DuckDuckGo integration (weather, financial, news, sports, politics)
- ✅ **Regional Language Detection** - Javanese, Sundanese, Batak, Minang, Bugis, Banjar
- ✅ **Context-Aware Replies** - Full conversation history always sent to LLM
- ✅ **Conversation Memory** - Multi-turn history per sender (10 exchanges, 1h TTL)
- ✅ **Rate Limit Handling** - Cooldown/backoff on 429 errors
- ✅ **Quote Context Extraction** - Extracts quoted/replied message text for LLM context

### **Dashboard & Monitoring**
- ✅ **Web UI** - FastAPI dashboard at http://127.0.0.1:8899
- ✅ **Real-time Logs** - Server-Sent Events (SSE) with phone masking
- ✅ **LLM Switching** - Hot-swap providers (Gemini/Groq/Ollama)
- ✅ **Ollama Control** - Model selector + keep-alive toggle
- ✅ **RAG Mode Toggle** - Switch between HYBRID/FULL RAG
- ✅ **Browser Selection** - Native (System Chrome) vs Bundled (Playwright)
- ✅ **Headless Mode** - CPU savings 30-40%
- ✅ **Ignore Groups Toggle** - Hot-swap ON/OFF without restart
- ✅ **Statistics** - Chat analytics with Plotly charts
- ✅ **API Key Management** - Add/Edit/Delete keys with rotation
- ✅ **Knowledge Base Management** - Upload documents, add websites, query, delete
- ✅ **Analytics Page** - Real-time WebSocket updates, KPI summary, daily stats, top senders
- ✅ **System Information** - OS, uptime, kernel, platform display
- ✅ **WhatsApp Status Display** - Connection, session, uptime, messages, errors
- ✅ **Pause/Resume Control** - Optional auto-resume timer (duration in minutes)
- ✅ **Auto-detect Running Agent** - Scans psutil to detect agent started outside dashboard
- ✅ **SPA Architecture** - Single-page app with catch-all routing
- ✅ **WhatsApp Status Broadcast** - WebSocket broadcasts of connection status changes

### **Analytics & Database**
- ✅ **SQLite Database** - Dual-write (text files + SQLite simultaneously)
- ✅ **Response Latency Tracking** - IN-to-OUT timestamp calculation (p50, p95, avg, min, max)
- ✅ **Message Analytics** - Daily stats, top senders, chat type distribution, peak hours
- ✅ **Activity Heatmap** - Hour x day of week visualization
- ✅ **Group Statistics** - Message count, unique senders per group
- ✅ **Recent Activity Feed** - Real-time WebSocket updates
- ✅ **Auto-migration** - Schema changes handled automatically
- ✅ **Database Views** - daily_stats, top_senders, group_activity

### **RAG Knowledge Base**
- ✅ **Document Upload** - PDF, DOCX, TXT, MD support
- ✅ **Web Crawling** - Domain-restricted, depth-limited (max 20 pages)
- ✅ **Text Chunking** - 500-char chunks with 50-char overlap
- ✅ **Vector Search** - ChromaDB with cosine similarity
- ✅ **3 Operational Modes** - general_ai, smart_mode (RAG→LLM fallback), rag_only
- ✅ **Source Attribution** - Answers include source references
- ✅ **Confidence Threshold** - 0.75 minimum for RAG answers
- ✅ **Auto-cleanup** - Orphaned vector removal on document deletion
- ✅ **Real-time Mode Switching** - No restart required

### **Security & Access Control**
- ✅ **Bot Commands Disabled in Groups** - `/botoff`, `/boton` only in private
- ✅ **Authorization System** - BOSS_IDENTIFIERS and CONTROL_IDENTIFIERS
- ✅ **Banned Tokens** - `|`, `;`, `&&`, `||`, `>`, `<`, `$(`, backticks, `sudo`, etc.
- ✅ **Forkbomb Detection** - Pattern matching for dangerous commands
- ✅ **AI Output Cleaning** - Removes quotes, backticks, markdown, comments
- ✅ **Sensitive Keyword Blocking** - Passwords, OTP, PIN, bank accounts, KTP, NIK, NPWP
- ✅ **Ignored Chats** - Official WhatsApp accounts filtered out
- ✅ **Privacy-First Logging** - Phone number masking in all logs

### **Logging & Monitoring**
- ✅ **Multi-Destination Logging** - TXT, JSONL, SQLite, Console, WebSocket
- ✅ **Log Rotation** - Daily rotation with configurable retention (90/30/7 days)
- ✅ **Gzip Compression** - Old logs compressed automatically
- ✅ **Color-Coded Console** - Green=private, blue=group, cyan=out, purple=group out, red=errors
- ✅ **Error Monitoring** - Rate tracking, alert thresholds, cooldown system
- ✅ **Health Service** - Unified health checks (Ollama, WA, Gemini, Groq, SQLite, Dashboard)
- ✅ **Error Report Generation** - JSON export with error type distribution

### **Memory & Planning**
- ✅ **Short-term Memory** - TTL-based (1 hour, max 100 items)
- ✅ **Long-term Memory** - Persistent JSON file storage
- ✅ **Task Planner** - Priority-based task creation (CRITICAL, HIGH, MEDIUM, LOW)
- ✅ **ReAct Loop Engine** - OBSERVE → THINK → ACT → OBSERVE → REFLECT cycle
- ✅ **Tool Registry** - Tool execution with max iteration limit
- ✅ **Step Trace Recording** - Full execution history

### **Architecture**
- ✅ **Modular Design** - Base classes (BaseAgent, BaseService, BaseTool)
- ✅ **DRY Principle** - Shared utilities, decorators, services
- ✅ **Event-Driven** - Pub/sub event bus with WebSocket real-time updates
- ✅ **Health Monitoring** - Built-in health checks with percentage summary
- ✅ **Error Handling** - 12 custom exception types
- ✅ **Privacy-First** - Phone number masking, local profile
- ✅ **Security** - Bot commands disabled in groups, authorization required
- ✅ **Message ID Generation** - UUID-based unique IDs for every message
- ✅ **Reply-to-Message Tracking** - Links OUT to triggering IN message

---

## 🔧 Configuration

### API Keys
Edit files in `config/keys/`:
- `gemini_keys.txt` - Google Gemini API keys
- `groq_key.txt` - Groq API key

### WhatsApp Profile
Default: `wa_profile/`
- Persistent browser profile
- Login session saved
- No need to scan QR every time

---

## 🛠️ Development

### **Coding Standards**

This project follows **DRY (Don't Repeat Yourself)** principle with modular architecture:

- **Use Base Classes:** `BaseAgent`, `BaseService`, `BaseTool` from `shared/bases.py`
- **Type Hints:** Always use type hints for function signatures
- **Error Handling:** Use custom exceptions from `shared/errors.py`
- **Logging:** Use centralized logging from `logging_utils.py`

### **Adding New Features**

1. **Create in shared/:** Base class implementation
2. **Register in agent:** Import and initialize in `WhatsAppAgent`
3. **Add API endpoint:** If needed, add in `dashboard/routes/api.py`
4. **Add UI:** If needed, add in `templates/index.html` + `static/js/`

### **Testing**

```bash
# Run unit tests (if available)
pytest tests/

# Test LLM connection
python scripts/test_ollama.py

# Test API endpoints
curl http://127.0.0.1:8899/api/status
```

### **For AI Assistants**

📘 **Read [`AI_INSTRUCTION.md`](AI_INSTRUCTION.md) first!** It contains:
- Complete architecture overview
- Core systems explanation (RAG, Multi-LLM, WhatsApp Bot)
- Development guidelines & best practices
- Troubleshooting guides
- API reference
- Checklist for understanding the project

---

## 🆕 Latest Updates

### **v3.0.0 - Focus on WhatsApp Bot Only (April 13, 2026)**

| Feature | Description | Benefit |
|---------|-------------|---------|
| **🗑️ Terminal Command Center Removed** | Removed /aitest command, dashboard terminal UI | Cleaner codebase, focused on WA ✅ |
| **🗑️ AI Chat Interface Removed** | Dashboard's separate LLM client removed | Simplified dashboard ✅ |
| **🎯 Project Rebranded** | UNIXwaBOT → WABro | Clear identity focus ✅ |

### **v2.9.0 - Multi-Turn Conversation Memory (April 11, 2026)**

| Feature | Description | Benefit |
|---------|-------------|---------|
| **🧠 Multi-Turn Memory** | LLM receives last 10 exchanges, not just 1 | Context-aware replies across full conversation ✅ |
| **📋 Always Injected** | History sent to LLM on EVERY message (no pronoun trigger needed) | LLM always knows conversation context ✅ |
| **🔄 Multi-Turn Format** | `User:` / `Assistant:` alternating format in prompt | LLM understands who said what ✅ |
| **⏱️ TTL-Based Expiry** | Entries expire after 1 hour automatically | Stale context auto-cleaned ✅ |
| **🔙 Backward Compatible** | `get_conversation()` still works (returns last exchange) | No breaking changes ✅ |

**Before:**
```
❌ Only 1 exchange stored per sender
❌ Context only sent if pronoun detected (dia, itu, nya, mereka)
❌ LLM blind to conversation history without pronouns
❌ Flat single-turn prompt — LLM confused about context
```

**After:**
```
✅ Up to 10 exchanges stored per sender (configurable)
✅ History ALWAYS sent to LLM — no pronoun trigger needed
✅ Multi-turn format: User/Assistant alternating
✅ LLM understands full conversation flow
✅ TTL 1 hour — old context auto-cleansed
```

**Example — What LLM Sees Now:**
```
Peran: Kamu adalah asisten AI untuk Pande Permadi.
Gaya: SANTAI, hangat, friendly...

--- RIWAYAT PERCAKAPAN ---
User: cuaca hari ini?
Assistant: Cerah 30°C.

User: kalau besok?
Assistant: Hujan 25°C dengan angin 15 km/h.
--- END RIWAYAT ---

Pesan pengguna: wind speed-nya?
```

### **v2.8.0 - Afternoon Improvements (March 13, 2026)**

| Feature | Description | Benefit |
|---------|-------------|---------|
| **🌐 Dashboard Port 8899** | Changed from 8000, configurable via .env | Avoid conflicts, easy config |
| **🚫 Ignore Groups Toggle** | Hot-swap ON/OFF without restart | Real-time control |
| **📤 Send Logging** | Enhanced debug for message failures | Track send issues |
| **🎨 Ollama Temp 0.8** | llama3.2:1b: 0.6 → 0.8 | More creative responses |
| **🌍 Bundled Browser** | Default: Playwright Chromium | 100% Windows compatible |

### **v2.7.0 - Latency Optimization (March 13, 2026)**

| Feature | Description | Benefit |
|---------|-------------|---------|
| **🧠 Emotional Core Removed** | Removed 4-layer emotional processing | **-50-200ms latency** ✅ |
| **⏱️ Typing Delay Removed** | No more artificial delay simulation | **-1-8s latency** ✅ |
| **🤖 Qwen API Removed** | Deleted paid API adapter | **Cleaner codebase** ✅ |
| **📋 LLM Adapters Simplified** | Removed emotional_metadata processing | **Faster response** ✅ |

### **v2.6.0 - Quality of Life Improvements**

| Feature | Description | Benefit |
|---------|-------------|---------|
| **🔌 Port 8899 Auto-Cleanup** | `wabro.sh` auto-kill port sebelum start | No more "Address in use" errors |
| **🎨 Guided Freedom** | Temperature 0.8, creative responses | Varied, natural, human-like replies |

---

## ⚠️ Compliance

**Important:** This project uses WhatsApp Web automation via Playwright (not official API).

**Risks:**
- May violate WhatsApp Terms of Service
- Could result in account restrictions
- UI changes may break automation

**Recommendation:** Use official [WhatsApp Business Platform](https://business.whatsapp.com/) for production.

---

## 📝 License

Internal project - WABro

---

## 👨‍💻 Author

Pande Permadi (unixlab)
