# NFT Market Intelligence Dashboard

> Real-time NFT market insights powered by the OpenSea API

A lightweight analytics tool for tracking NFT collection performance, floor price movements, sales volume trends, and market events — built on top of the OpenSea V2 API.

---

## Overview

This project queries the OpenSea API to surface actionable market data for NFT collectors, traders, and researchers. It is designed as a personal research and analytics tool, not a commercial product or trading bot.

**Key goals:**
- Track real-time floor prices and volume across top collections
- Monitor listing and sale events via the OpenSea WebSocket stream
- Aggregate collection-level statistics for trend analysis
- Export clean data snapshots for offline research

---

## Features

- Collection stats: floor price, 7d/30d volume, market cap, number of owners
- Sales event feed: live and historical sales by collection
- NFT metadata lookup by contract address and token ID
- WebSocket listener for real-time listing and offer events
- CSV export for research and charting

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Python 3.11+ |
| HTTP Client | `httpx` (async) |
| WebSocket | `websockets` |
| Data | `pandas` |
| Storage | SQLite (local) |
| Scheduling | `APScheduler` |

---

## Project Structure

```
nft-market-intelligence/
├── src/
│   ├── client.py          # OpenSea API V2 wrapper
│   ├── websocket.py       # Real-time event stream listener
│   ├── collections.py     # Collection stats fetcher
│   ├── events.py          # Sales/listing event parser
│   └── export.py          # CSV and SQLite export helpers
├── data/                  # Local data snapshots (gitignored)
├── notebooks/             # Jupyter analysis notebooks
├── tests/
├── .env.example
├── requirements.txt
└── README.md
```

---

## Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/YOUR_USERNAME/nft-market-intelligence.git
cd nft-market-intelligence
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure your API key

Copy `.env.example` to `.env` and add your OpenSea API key:

```bash
cp .env.example .env
```

```env
OPENSEA_API_KEY=your_key_here
```

> **Note:** You can run this project without an API key in development mode — rate limits apply but all endpoints are accessible.

### 4. Fetch collection stats

```python
from src.client import OpenSeaClient

client = OpenSeaClient()
stats = client.get_collection_stats("pudgy-penguins")
print(stats)
```

### 5. Listen to live events

```python
from src.websocket import EventStream

stream = EventStream(collection_slug="boredapeyachtclub")
stream.listen()  # Prints incoming listings, offers, and sales
```

---

## API Reference

This project uses the [OpenSea API V2](https://docs.opensea.io/reference/api-overview). Relevant endpoints:

| Endpoint | Description |
|---|---|
| `GET /collections/{slug}/stats` | Floor price, volume, supply, owners |
| `GET /events/collection/{slug}` | Sales and listing history |
| `GET /nfts/{chain}/{address}/{id}` | NFT metadata |
| `WS /` | Real-time event stream |

---

## API Key

This project requires an OpenSea API key for production use. Apply here:
[https://docs.opensea.io/reference/api-keys](https://docs.opensea.io/reference/api-keys)

---

## Roadmap

- [ ] Dashboard UI (Streamlit or Flask)
- [ ] Multi-collection comparison view
- [ ] Price alert notifications (Discord webhook)
- [ ] Historical floor price charts
- [ ] Rarity scoring integration

---

## License

MIT — personal and research use only. This project is not affiliated with OpenSea.
