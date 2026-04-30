# MyLA311 Search (CA) v1.35

MyLA311 uses the public SODA API from data.lacity.org to look up service request information. To avoid confusion between different versions of the same address—such as “200 N Spring St, Los Angeles, CA 90012” versus “200 Spring St”—the system converts the address into GPS coordinates. This helps the app find the correct location and identify nearby issues more accurately.

The application allows users to enter a full or partial address, a City issue number, or a landmark name such as “City Hall.” The results appear in a pop‑up window. Users can also filter the information by issue category, year, and request status (open, closed, or cancelled) directly from the interface.

![Demo](./MyLA311_CA_Demo.gif)

## What This App Does

- Searches by address or SR number against `data.lacity.org / MyLA311` datasets.
- Uses multi-year fan-out across 12 datasets (`2015-2026`).
- Filters results by status (Open/Closed/Cancelled) and year buckets (`2026`, `2025`, `2024`, `2023`, `2022-Prior`).
- Shows interactive map markers, nearby radius results, and a popup results window.
- Lets users copy SR numbers and open result addresses directly in Google Maps.

## Using The App

1. Enter an address or SR number.
2. Select radius and optional date range.
3. Click `Find Nearby Issues`.
4. Use status/year/type filters to narrow results.
5. Click an SR badge to copy the SR number.
6. Click the address line to open Google Maps for that location.

## 🥤SODA Configuration

- `App Token` is optional but recommended to reduce throttling.
- `Max results per year` controls per-dataset fetch size.
- `Last updated` shows the latest date detected from the configured SODA dataset.

## Application Logic Overview

### Desktop Launcher (`desktop.py`)
- **Purpose:** Starts a local Flask server and launches the app in a browser or desktop window.
- **How it works:**
	1. **ServerThread:** Runs the Flask app in a background thread using Werkzeug.
	2. **wait_for_server:** Waits for the server to be ready before launching the UI.
	3. **UI Launch:** 
		 - If `pywebview` is available, opens the app in a desktop window.
		 - Otherwise, opens the app in the default web browser and shows a Tkinter info window.
	4. **Shutdown:** Ensures the server is stopped when the app closes.

### Flask App (`app.py`)
- **Purpose:** Handles all backend logic, API calls, and data processing.
- **Key features:**
	- Uses SODA API to fetch MyLA311 service request data from multiple yearly datasets.
	- Converts user input (address, SR number, or landmark) to GPS coordinates for accurate search.
	- Supports filtering by status, year, and issue type.
	- Returns results for display on an interactive map and in a results window.

---

## Developer Audit Log

**2026-04-30**
- Removed unused imports from benchmark_fanout.py and mapvisualizerv1_4b.py
- Verified no unused variables or functions remain in main project files
- Added application logic summary and audit log to README.md

## Version History
- v1.35: Performance tune and logic clean up.
- v1.3: Added support for search by using landmark.
- v1.2: Added support for filter logic.
- v1.1: Added support for 2025b dataset (73a2-6ar5, v2026 schema) in address/radius search and UI filter logic.
- v1.0: Initial version with SODA live data, multi-year support, and UI filters.


