# n8n Weather Alert Automation

An automated weather monitoring workflow built with **n8n** that fetches a 5-day forecast from the OpenWeather API every morning and delivers a summary directly to your Gmail inbox — no code, no backend, just a fully workflow-driven automation.

---

## How It Works

The workflow runs automatically at **10:00 AM daily** using n8n's Schedule Trigger. It pulls a 5-day forecast for your configured location from OpenWeather API, extracts the current temperature, temperature range, and wind speed, then formats and sends a clean weather summary to your Gmail.

```
Schedule Trigger (10:00 AM)
        │
        ▼
OpenWeatherMap Node
(5-day forecast, zip code)
        │
        ▼
Gmail Node
(sends formatted weather summary)
```

### Sample Email Output

```
Subject: Today's Weather Report

Good morning! The current temperature is 28°C in Faridabad.
Temperature range: 22°C to 34°C
Wind speed: 4.2 m/s
```

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| n8n | Workflow automation engine |
| OpenWeather API | Real-time weather + 5-day forecast data |
| Gmail API (OAuth2) | Email delivery |

---

## Prerequisites

- n8n installed (self-hosted or cloud)
- OpenWeather API key — free at [openweathermap.org](https://openweathermap.org/api)
- Gmail account with OAuth2 credentials configured in n8n

---

## Setup Instructions

### Step 1 — Import the workflow

1. Open your n8n instance
2. Go to **Workflows → Import**
3. Upload `My workflow 3.json` from this repo
4. The workflow will load with all three nodes pre-configured

### Step 2 — Add OpenWeather credentials

1. Click the **OpenWeatherMap** node
2. Under Credentials, click **Create New**
3. Paste your OpenWeather API key
4. Save

### Step 3 — Configure your location

In the **OpenWeatherMap** node, update the zip code to your city:

```
Zip Code: YOUR_ZIPCODE,IN
```

Example: `110001,IN` for New Delhi, `400001,IN` for Mumbai

### Step 4 — Add Gmail credentials

1. Click the **Gmail** node
2. Under Credentials, select or create a Gmail OAuth2 connection
3. Update the `sendTo` field to your email address

### Step 5 — Activate

Toggle the workflow to **Active**. It will now run every day at 10:00 AM automatically.

---

## Customisation

**Change the trigger time** — Open the Schedule Trigger node and update `triggerAtHour` to any hour (0–23).

**Change alert conditions** — Add an **IF node** between OpenWeatherMap and Gmail to only send alerts when temperature exceeds a threshold or rain is detected. Example condition: `{{ $json.list[0].main.temp }} > 40`

**Add more data** — The OpenWeather response includes humidity, weather description, feels-like temperature, and more. Edit the Gmail message template to include any fields from `$json.list[0]`.

---

## Project Structure

```
n8n-weather-alert-automation/
│
├── My workflow 3.json     # Importable n8n workflow file
├── README.md              # This file
└── LICENSE                # MIT License
```

---

## About

Built by **Amit Kumar Pal** — MCA student at Amity University, building AI automation workflows and DevOps projects.

- LinkedIn: [linkedin.com/in/amit-pal-1300ba260](https://www.linkedin.com/in/amit-pal-1300ba260/)
- GitHub: [github.com/amitpal3206](https://github.com/amitpal3206)

---

## License

MIT — free to use, modify, and distribute.
