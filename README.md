# OSIRIS Intelligence Tracking

Automated data extraction from the **OSIRIS** open-source intelligence platform (https://osirisai.live, v4.2).

## Data Sources (16 endpoints)

| File | Endpoint | Volume |
|------|----------|--------|
| `flights.json` | `/api/flights` | ~13K aircraft |
| `satellites.json` | `/api/satellites` | ~19K objects |
| `cctv.json` | `/api/cctv` | ~21K cameras |
| `maritime.json` | `/api/maritime` | ports + chokepoints |
| `earthquakes.json` | `/api/earthquakes` | USGS events |
| `fires.json` | `/api/fires` | NASA FIRMS |
| `weather.json` | `/api/weather` | NASA EONET |
| `conflicts.json` | `/api/conflicts` | warzones/maps |
| `country-risk.json` | `/api/country-risk` | risk scores |
| `cyber-threats.json` | `/api/cyber-threats` | CISA KEV |
| `infrastructure.json` | `/api/infrastructure` | nuclear facilities |
| `markets.json` | `/api/markets` | indices/stocks/crypto |
| `news.json` | `/api/news` | telegram/wire sources |
| `live-news.json` | `/api/live-news` | YouTube feeds |
| `gdelt.json` | `/api/gdelt` | global events |
| `space-weather.json` | `/api/space-weather` | Kp index/solar |
| `stats.json` | `/api/stats` | live counts |

See `OSIRIS_COMPLETE_REPORT.txt` for the full summary.

## Quick Re-fetch Script

```bash
pip install requests
python3 - << 'PY'
import json, requests, os
ENDPOINTS = ["flights","satellites","cctv","maritime","earthquakes","fires",
             "weather","conflicts","country-risk","cyber-threats","infrastructure",
             "markets","news","live-news","gdelt","space-weather","stats"]
os.makedirs("data", exist_ok=True)
for ep in ENDPOINTS:
    r = requests.get(f"https://osirisai.live/api/{ep}", timeout=30)
    with open(f"data/{ep}.json","w") as f:
        json.dump(r.json(), f, indent=2)
    print(f"✓ {ep}")
PY
```

