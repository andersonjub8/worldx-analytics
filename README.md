# WORLDX Analytics

Production-oriented BRC20-Prog analytics dashboard for WORLDX on Bitcoin.

## Stack
- Next.js + TypeScript
- Recharts
- Server-side UniSat API integration
- Responsive dark analytics UI
- CSV export
- Whale concentration and holder distribution calculations

## Data source
WORLDX is treated as a BRC20-Prog ticker. The app uses:
- `/v1/indexer/brc20-prog/{ticker}/info`
- `/v1/indexer/brc20-prog/{ticker}/holders`
- `/v1/indexer/brc20-prog/{ticker}/history`
- `/v1/indexer/brc20-prog/bestheight`
- `/v1/price/btc`

UniSat requires an API key for its Open API. Keep the key on the server.

## Run
1. Copy `.env.example` to `.env.local`
2. Set `UNISAT_API_KEY`
3. `npm install`
4. `npm run dev`
5. Open `http://localhost:3000`

## Important
The holder endpoint is paginated. The backend walks all holder pages so concentration/distribution calculations are based on the indexed holder set returned by UniSat. For very large holder sets, move synchronization into a scheduled worker and database.

## Production upgrade
Use PostgreSQL/Timescale or ClickHouse for historical snapshots. Store:
- token snapshots
- holder snapshots
- daily/hourly volume
- price candles
- indexer heights
- raw API payloads

This repository intentionally keeps the first version self-contained and deployable without a separate worker.
