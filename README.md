
# Network-Based Disease Spread Simulation Using Graph Algorithms

## Overview
This project is a **Data Structures and Algorithms (DSA) based simulation system** that models the spread of an infectious disease (such as COVID-19) across a social network. The social network is represented as a **graph**, where individuals are nodes and social interactions are edges.

The simulation demonstrates how diseases propagate through communities using classical graph traversal techniques and probabilistic models like **SIR (Susceptible–Infected–Recovered)**. Results are visualized interactively on a map and through epidemic curves.

---

## Objectives
- Apply **graph data structures** to a real-world problem
- Simulate disease spread using **network-based algorithms**
- Visualize infection dynamics over time
- Analyze efficiency, scalability, and algorithmic complexity

---

## Core Concepts Used
- Graphs (Adjacency Lists)
- BFS-style propagation
- Sets, Queues, and Dictionaries
- Probabilistic simulation
- Time & space complexity analysis

---

## Tech Stack

### Backend
- **Python**
- **FastAPI**
- **NetworkX** (graph creation & traversal)
- SIR / SEIR disease models

### Frontend
- **React + TypeScript**
- **Vite**
- **Google Maps JavaScript API**
- **Recharts** (SIR curves & statistics)
- Optional: **Deck.gl** for advanced visual layers

---

## Project Structure
DiseaseSpreadSimulation/
│
│├── backend/
│   ├── venv/                # Python virtual environment
│   ├── __pycache__/         # Python cache files
│   │
│   ├── api_schemas.py       # Pydantic schemas for API requests/responses
│   ├── config.py            # Global configuration (constants, settings)
│   ├── graph_gen.py         # Social network graph generation logic
│   ├── main.py              # FastAPI app entry point
│   ├── models.py            # Data models (SIR states, node structures)
│   ├── sim_logic.py         # Core disease spread simulation (SIR model)
│   ├── spatial.py           # Spatial / location-based node handling
│   ├── stores.py            # In-memory data storage for simulation state
│   └── utils.py             # Helper and utility functions
│
├── frontend/
│   ├── public/              # Static assets
│   ├── src/                 # React source code
│   │
│   ├── .env                 # Environment variables (Google Maps API key)
│   ├── .gitignore           # Git ignore rules
│   ├── README.md            # Frontend-specific documentation
│   ├── eslint.config.js     # ESLint configuration
│   ├── index.html           # Main HTML entry
│   ├── package-lock.json    # Dependency lock file
│   ├── package.json         # NPM dependencies and scripts
│   ├── postcss.config.js    # PostCSS configuration
│   ├── tailwind.config.js   # Tailwind CSS configuration
│   └── vite.config.js       # Vite build and dev server config
│ ├── requirements.txt
│ └── README.md

---

## How the Simulation Works

### Social Network as a Graph
- Each person is a **node**
- Each social interaction is an **edge**
- The graph is stored using **adjacency lists** (via NetworkX)

### Disease Model (SIR)
Each node is always in one of three states:
- **S (Susceptible)** – Healthy but can be infected
- **I (Infected)** – Currently infected
- **R (Recovered)** – Immune / no longer infectious

### Spread Logic
- The simulation runs in **discrete time steps** (days)
- At each step:
  - Infected nodes attempt to infect susceptible neighbors
  - Infection happens with probability `p`
  - Nodes recover after a fixed time or probability

### Algorithms Used
- **BFS-style propagation** using a queue
- Neighbor traversal: `O(degree(node))`
- Efficient updates by tracking only infected nodes
- Optional DFS/BFS for analysis (components, paths)


## Metrics & Analysis
During simulation, we record:
- New infections per day
- Total infected population
- Recovered individuals
- Epidemic peak timing
- Approximate basic reproduction number (R₀)

These metrics are plotted as **SIR curves** in real time.

## Visualization
- Nodes displayed on **Google Maps**
- Color-coded states:
  - 🟢 Susceptible
  - 🔴 Infected
  - 🔵 Recovered
- Charts show infection trends over time

### How to Run the Project

## Prerequisites
Make sure you have the following installed:
Python 3.9+
Node.js 18+
npm
(Optional but recommended) Git

## Run the Backend (FastAPI)

Open a terminal in the folder that contains DiseaseSpreadSimulation/, then run:

# cd DiseaseSpreadSimulation/backend

1. Create and activate a virtual environment
  -python -m venv venv
  -source venv/bin/activate        # macOS/Linux
# venv\Scripts\activate         # Windows PowerShell

2. Install backend dependencies
  -pip install -r ../requirements.txt

3. Start the FastAPI server
uvicorn main:app --reload --host 0.0.0.0 --port 8000

4. Test the backend
    Open your browser and visit:
       Swagger UI:
       http://localhost:8000/docs

   Health check:
       http://localhost:8000/health
# Expected response:
{"ok": true}

## Run the Frontend (React + Vite)

Open a second terminal, starting again from the project root:

cd DiseaseSpreadSimulation/frontend

1. Install frontend dependencies
npm install

2. Start the Vite development server
npm run dev


Vite will print a URL similar to:

http://localhost:5173/


Open this URL in your browser.

Confirm Backend–Frontend Connection

The frontend communicates with the backend at:

http://localhost:8000


Ensure:

Backend is running on port 8000

Frontend is running on port 5173

If both are running correctly, the simulation dashboard should load.

Common Issues & Quick Fixes
Backend import or module errors

Make sure that you:

Run uvicorn from the backend/ directory

Use the command:

uvicorn main:app --reload


❌ Do not run from inside individual Python files
❌ Do not run from the project root directory

Google Maps shows blank / “For development purposes only”

Check that:

Your Google Maps API key is valid

Billing is enabled on your Google Cloud project

Your API key must be placed in:

DiseaseSpreadSimulation/frontend/.env


Example:

VITE_GOOGLE_MAPS_KEY=your_api_key_here


After changing .env, restart the frontend:

npm run dev

Port already in use

Run the backend on a different port:

uvicorn main:app --reload --port 8001


Then update the frontend API base URL (for example, in src/App.jsx):

const API_BASE_DEFAULT = "http://localhost:8001";


Restart the frontend afterward.
