# Real-Time Drone Telemetry Dashboard with REST API
A full-stack application that simulates, ingests, stores, and visualizes real-time telemetry data from a drone. The project features a Node.js backend with a REST API, a persistent SQLite database, and a live-updating web dashboard built with WebSockets and Leaflet.js.

## ✨ Key Features
- **Real-Time Data Ingestion**: A robust Express.js server endpoint to receive high-frequency telemetry data.
- **Persistent Storage**: Telemetry data is permanently stored in a lightweight SQLite database, surviving server restarts.
- **Live Dashboard with WebSockets**: A front-end dashboard that connects to the server via WebSockets (socket.io) to receive and display data instantly without needing to refresh the page.
- **Interactive Map**: Uses Leaflet.js to display the drone's real-time position on a map, complete with a marker and a dynamically drawn flight path.
- **RESTful API**: Provides clear API endpoints to retrieve the latest status or the complete flight history of any drone.
- **Modular & Scalable**: A clean separation between the data simulator, the backend server, and the front-end dashboard.

## 🛠️ Technology Stack
- **Backend**: Node.js, Express.js, Socket.IO, CORS
- **Database**: SQLite3
- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **Libraries**:
    - axios (for the drone simulator)
    - leaflet.js (for the interactive map)


## 🏗️ Project Architecture
The application is composed of three main components that run independently:
- **Drone Simulator (drone_simulator.js)**: A Node.js script that simulates a drone's flight. It periodically sends its telemetry data (ID, location, altitude, battery) via a POST request to the API Server.
- **API Server (index_database.js)**: The core of the application. It receives data from the simulator, stores it in the SQLite database, and pushes it out in real-time to any connected dashboard clients via WebSockets. It also serves the front-end files and provides REST endpoints for historical data.
- **Dashboard (public/)**: A static front-end application that runs in the user's browser. It establishes a WebSocket connection to the server to receive live updates and visualizes the data on a map and status panel.

```
+----------------------+      +----------------------+      +----------------------+
|                      |      |                      |      |                      |
|  Drone Simulator     |----->|  Node.js API Server  |----->|  SQLite Database     |
| (drone_simulator.js) | POST |  (index_database.js) |      |   (telemetry.db)     |
|                      |      |                      |      |                      |
+----------------------+      +----------+-----------+      +----------------------+
                                         |
                                         | (WebSocket Push)
                                         v
                              +----------+-----------+
                              |                      |
                              |    Live Dashboard    |
                              |   (Browser Client)   |
                              |                      |
                              +----------------------+
```                        

## 📁 Project Structure
The project is organized to separate the core backend logic from the front-end dashboard and the data simulator.

```
.
├── public/
│   ├── index.html          # The HTML structure for the dashboard
│   └── main_connect.js             # Client-side JS for map and WebSocket logic
├── database_setup.js       # One-time script to create the SQLite database and table
├── drone_simulator.js      # Simulates a drone sending telemetry data
├── index_database.js                # The main Node.js server (Express + Socket.IO)
├── package.json
└── telemetry.db            # The SQLite database file (created by the setup script)
```


## 🚀 Getting Started
Follow these instructions to get the project up and running on your local machine.

**Prerequisites**
+ Node.js (which includes npm) installed on your system.

**Installation & Setup**
1. Clone the repository:

```
    git clone https://github.com/JKit-66/realtime-drone-telemetry-api-dashboard.git
```

2. Install project dependencies:

```
    npm install
```

3. Set up the database:
Run the setup script once to create the telemetry.db file and the necessary table.
```
    node database_setup.js
```

**Running the Application**
You will need to run two processes in two separate terminal windows.

1. Start the Server:
In your first terminal, start the main Node.js server. You should see console logs confirming the server is running and connected to the database.

```
    node index_database.js
```

2. Start the Drone Simulator:
In your second terminal, start the drone script. You will see logs confirming that telemetry data is being sent.

```
    node drone_simulator.js
```


3. View the Dashboard:
To see the live dashboard, with the map and status panel updating in real-time, open your web browser and navigate to:
http://localhost:3000


## 📡 API Endpoints
The server exposes the following RESTful API endpoints for querying historical data:

- ``` POST /api/telemetry ```
    - Receives a new telemetry packet from a drone.
    - Body: ```{ "droneId": "string", "lat": number, "lon": number, "altitude": number, "battery": number }```

- ``` GET /api/drones/:id/status ```
    - Returns the most recent telemetry packet for the specified ```droneId```.

- ```GET /api/drones/:id/history ```
    - Returns an array of all historical telemetry packets for the specified ```droneId```.

📄 License
This project is licensed under the MIT License - see the ```LICENSE``` file for details.