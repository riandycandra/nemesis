# Nemesis
Nemesis is the public-facing investigative interface as the result of Operation Diponegoro, initiated by Abil Sudarman School of Artificial Intelligence. We ingest millions of rows of procurement data, surface anomalies, and make the findings legible to citizens, journalists, and policymakers.

Live dashboard: https://assai.id/nemesis


> End the vampire ball.


## Release Status

| Asset | Status | ETA |
|-------|--------|-----|
| Fine-tuned model | 🟡 In progress | ? |
| Scraping & Analyze source code | 🟡 In progress | ? |



Stay tuned.

## Downloads

### Dataset

[Download SIRUP raw jsonl dataset (analyzed by GPT-5.4)](https://contenflowstorage.blob.core.windows.net/shared/gpt-5.4-analyzed-sirup.zip?sp=r&st=2026-04-16T12:00:08Z&se=2029-04-16T20:15:08Z&spr=https&sv=2025-11-05&sr=b&sig=m%2FATynnnZq5gSdP8xWWw2ew41EMJZz09fDQRwpbWolk%3D)

[Download SIRUP dataset SQL Ver (analyzed by GPT-5.4-mini)](https://contenflowstorage.blob.core.windows.net/shared/datasets/dashboard.sql?sp=r&st=2026-04-16T12:16:15Z&se=2029-04-16T20:31:15Z&spr=https&sv=2025-11-05&sr=b&sig=sKPH9uazyLcYcSwhARcEwVSG%2FTld9VnGJgZ2mOZIxrA%3D)


### Model
Stay tuned

### 1. Prepare the Database

Follow these steps to generate SQLite data locally:

1. Download and unzip the raw dataset from the links in the [Downloads](#downloads) section.
2. Move `.csv`, `.json`, and `.jsonl` files into `./backend/dataset`.
3. Initialize the database:
   ```bash
   cd backend
   npm install
   npm run db:reset
   ```

The backend expects the database at `backend/data/dashboard.sqlite`.

### 2. Run the Application

**1. Start the backend**

```bash
cd backend
npm start
```

The backend runs on `http://127.0.0.1:3000`.

**2. Serve the frontend** (in a second terminal)

```bash
cd frontend
python3 -m http.server 8080
```

Then open `http://127.0.0.1:8080` in your browser.

The frontend is preconfigured to call the backend at `http://127.0.0.1:3000/api`.

### 3. Run with Docker

You can run both services with Docker Compose:

```bash
docker compose up -d --build
```

- Frontend: `http://localhost:8080`
- Backend API: `http://localhost:3000/api`

Notes:
- Complete **Step 1** first so `backend/data/dashboard.sqlite` exists.
- Compose default sets `CORS_ORIGIN=http://localhost:8080` (override with env var if needed).

## Notes

- No frontend build step required — plain HTML/CSS/JS.
- If `backend/node_modules` is missing, install dependencies:
```bash
  cd backend
  npm install
```
- For development mode with hot reload:
```bash
  cd backend
  npm run dev
```

## Environment

Backend config is loaded from `backend/.env`. Default values:

```env
PORT=3000
CORS_ORIGIN=*
SQLITE_PATH=data/dashboard.sqlite
AUDIT_DATASET_DIR=dataset
GEO_ROOT_PATH=seed/geo
```
