# Contextual background

In Brazil, every infrastructure project with medium/high environmental impact must have an environmental license. In order to do that, one of the steps is to estimate the trade-off needed depending on the impact caused. The math for doing that is relatively straightforward, however, each municipality has its owns rules of trade-off, and there is not a unified platform where the consultants can check the value per type of intervention, and per location. Usually this is a very manual process, where consultants need to visit governmental websites and go through multiple PDFs. Thus, the main motivation of this project is to create an unique platform where the consultants can go and get the trade-off values per type and location of intervention.

# Environmental Trade-off Calculator – Frontend

This repository contains only the web interface for the *Environmental Trade-off Calculator*, which communicates with a separate Flask API (backend) to estimate environmental compensation for isolated trees, forest patches, PPA areas, and to query species conservation status.

All backend setup (Python, virtualenv, database, CSV loading, Swagger, etc.) is documented in the backend’s own README.  
This README focuses only on the frontend.

---

## Technologies

- page structure (`index.html`)
- layout and styling (`styles.css`)
- UI logic and API calls (`scripts.js`)

---

## Features

The main page (`index.html`) is organized into tabs, one for each workflow:

### 1. Isolated trees

**Tab:** `Isolated trees`

- **Inputs:**
  - Quantity of trees  
  - Group (native / exotic)  
  - Municipality (from a dropdown loaded via API)  
  - Whether the species is endangered or not (true/false dropdown)

- **Behavior:**
  - Each added item is listed in a table.
  - When you click “Calcular compensação”, the frontend:
    - sends all items to the backend
    - shows compensation per tree
    - shows total compensation per item
    - shows the total compensation for the entire lot at the bottom of the tab.

---

### 2. Patch / area (m²)

**Tab:** `Patch / area (m²)`

- **Inputs:**
  - Municipality (dropdown loaded via API)  
  - Patch area in m²  

- **Behavior:**
  - Each patch is added as a row in a table.
  - When you click “Calcular compensação”, the frontend:
    - calls the API to get the compensation factor per m²
    - shows compensation per m²
    - shows total compensation for each patch
    - shows the total compensation for all patches in the tab.

---

### 3. PPA

**Tab:** `PPA`

- **Inputs:**
  - Municipality (dropdown loaded via API)  
  - Quantity/area to compensate  

- **Behavior:**
  - Each PPA entry appears in a table.
  - On “Calcular compensação”, the frontend:
    - calls the PPA endpoint in the backend
    - displays compensation per unit**
    - displays the total PPA compensation** for all entries.

---

### 4. Species status

**Tab:** `Species status`

- **Inputs:**
  - Family (e.g. `ACANTHACEAE`)
  - Scientific species name (e.g. `Aphelandra squarrosa Nees`)

- **Behavior:**
  - Sends a GET request to the backend.
  - Displays:
    - Family  
    - Species  
    - Conservation status (EW, CR, EN, VU, etc.)  
    - A short description of the status.

---

## API Endpoints Used

The frontend communicates with the backend using `fetch`.  
The base URL is configured in `scripts.js` as:

```js
const API_BASE = "http://127.0.0.1:5002";
