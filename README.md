# 🐙 TentaTrend

TentaTrend is a single-page crypto dashboard built as a CS passion project. It tracks live prices, momentum signals, news, and price alerts for coins listed on both Coinbase and Crypto.com — no backend, no build step, no API keys. Just open the page.

> **Not financial advice.** Nobody can reliably predict crypto prices. The "trend signal" here is a basic 7-day/21-day moving-average crossover, included for learning purposes, not trading decisions.

## Features

- **Prices** — live prices, 24h change, and a 30-day sparkline for 8 major coins (BTC, ETH, SOL, ADA, DOGE, LINK, LTC, DOT), each with a momentum signal and a detail view (chart, market cap, volume, high/low, circulating supply, ATH)
- **Trade links** — direct links to each coin's page on Coinbase and Crypto.com
- **News** — live headlines aggregated from CoinDesk and Cointelegraph
- **Whales** — news headlines filtered for large-transaction / whale-related coverage (see [Data sources](#data-sources) for why this isn't raw on-chain data)
- **Alerts** — set a price threshold per coin; get a browser notification when it's crossed, checked entirely client-side
- **Inky** — a support assistant with three layers: a fixed FAQ (instant, free, no key needed), live data-aware answers for "how's BTC doing" style questions pulled straight from the already-loaded price/signal data, and an *optional* real-AI mode where you supply your own Anthropic API key and open-ended questions go straight from your browser to Claude

## Tech stack

Plain HTML, CSS, and vanilla JavaScript. No frameworks, no build tools, no dependencies to install. Fonts load from Google Fonts via CDN.

## Data sources

| Data | Source |
|---|---|
| Prices, 30-day history, market stats | [CoinGecko API](https://www.coingecko.com/en/api) (public, no key) |
| News | [CoinDesk](https://www.coindesk.com/) and [Cointelegraph](https://cointelegraph.com/) RSS, converted via [rss2json.com](https://rss2json.com/) |
| Whale activity | Same news feed, filtered client-side for whale-related keywords — genuinely free, keyless, on-chain whale-transaction APIs don't really exist; the real ones (e.g. Whale Alert) require a paid key |
| Inky's real-AI mode (optional) | [Anthropic API](https://docs.claude.com/en/api/overview) — only called if you turn this on in ⚙ settings and paste in your own API key; off by default |

All requests are made directly from the browser (no server), so all of the above must support CORS for the app to work — they do at time of writing, but third-party APIs can change without notice. If a tab stops loading, check the browser console for the actual error.

## Running it

No install required.

```bash
git clone https://github.com/<your-username>/tentatrend.git
cd tentatrend
```

Then just open `index.html` in a browser, or serve it locally:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

### Deploying with GitHub Pages

1. Push this repo to GitHub.
2. Go to **Settings → Pages**.
3. Set **Source** to the `main` branch, root folder.
4. Your dashboard will be live at `https://<your-username>.github.io/<repo-name>/`.

## Known limitations

- Free public APIs are rate-limited; heavy refreshing may temporarily fail.
- Inky's FAQ and data-aware replies run on fixed keyword matching against already-loaded data, not a language model.
- Inky's optional real-AI mode calls the Anthropic API directly from the browser with a key you paste in yourself. That key lives only in that tab's memory and is never sent anywhere but Anthropic — but pasting any API key into a client-side page has real exposure if you're on a shared or compromised machine, so use a key you're comfortable putting at risk, and it's forgotten on refresh/close.
- Browser notifications for Alerts require the page to stay open in a tab.

## Contributing

This started as a personal CS project, but pull requests (new tabs, more coins, a real backtested signal, etc.) are welcome — open an issue first if it's a bigger change.

## License

MIT — see [LICENSE](LICENSE).
