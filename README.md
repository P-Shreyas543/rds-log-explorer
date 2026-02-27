# RDS Log Explorer

A lightweight, completely client-side web application for querying, parsing, and visualizing RDS telemetry data from AWS Lambda. 

Because this tool runs entirely in the browser, there are no backend servers to configure (other than your existing Lambda endpoint) and no server-side CSV conversions required. Just open the file and start exploring your telemetry data.

## ✨ Features
* **Zero-Install:** A single `index.html` file containing all necessary HTML, CSS, and JavaScript.
* **Direct Lambda Integration:** Fetches NDJSON (Newline Delimited JSON) payloads directly from your configured AWS Lambda URL.
* **Interactive Telemetry Graphing:** Automatically detects numeric fields in your JSON payloads and plots them on an interactive, zoomable chart using Chart.js.
* **Local Parsing & Filtering:** Search through your data in real-time using the built-in text filter. 
* **Data Export:** Export your fetched, filtered data directly to CSV or download the raw JSONL file locally.

## 🚀 Quick Start (Local Use)
You do not need to host this file to use it. 
1. Clone or download this repository.
2. Double-click the `index.html` file to open it in any modern web browser (Chrome, Firefox, Edge, Safari).
3. Enter your Thing Name, select a date range, and click **Fetch & Parse Logs**.

## 🌐 Hosting on GitHub Pages
This project is perfectly suited for free hosting via GitHub Pages.
1. Upload `index.html` to a public GitHub repository.
2. Go to your repository **Settings** > **Pages**.
3. Under "Build and deployment", set the source to **Deploy from a branch**.
4. Select the `main` branch and click **Save**.
5. Your site will be live at `https://[your-username].github.io/[repo-name]/`.

## ⚠️ Important Configuration: CORS
If you are hosting this on GitHub Pages (or any other domain), your AWS Lambda endpoint **must** be configured to allow Cross-Origin Resource Sharing (CORS). 

If CORS is not configured, your browser will block the tool from fetching data. Ensure your Lambda function returns the following headers:
```http
Access-Control-Allow-Origin: * (Or specify your exact GitHub Pages URL)
Access-Control-Allow-Methods: POST, OPTIONS
Access-Control-Allow-Headers: Content-Type, Accept
```

## 🐛 Known Limitations
Large Dataset Freezing: Currently, processing massive datasets (e.g., querying 3+ days of telemetry data at once) happens synchronously on the browser's main thread. This may cause the browser window to temporarily freeze or crash.

Recommendation: Until background processing (Web Workers/Chunking) is implemented, it is highly recommended to keep your queries under 24 hours, or use the "Quick Range" buttons for 1-12 hour increments.
