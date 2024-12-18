# SPEEDOMETER APP


## Project Overview
The project consists of a backend service that manages the WebSocket connections and communicates with the front end, as well as a React-based dashboard displaying speed data. This application simulates speedometer data, sent periodically through WebSocket connections and displayed as a time series on a chart. The backend also stores the incoming data in a MySQL database.

## Architecture

The system consists of the following components:

#Frontend (React App):

- A React dashboard that establishes a WebSocket connection to the backend.
- Displays a line chart of speed values over time using Chart.js.
- Sends random speed data every second to the backend via WebSocket.

#Backend (Flask & WebSocket):

- A Flask-based REST API to handle HTTP requests.
- A WebSocket server to accept real-time data from the Frontend and broadcast the same data back to the sender.
- Stores the speed data in a MySQL database for future analysis.
  
#Database (MySQL):

- Stores speed and timestamp data sent from the Frontend for persistent storage.

#Dockerized Deployment

Each component (backend and frontend) is containerized with a Dockerfile.

Ensures consistent deployment across environments.

![sourcse code](https://github.com/user-attachments/assets/ece4d098-219b-417a-87f3-bcbd2b514194)


## System Flow

- **Frontend:**

On page load, the React app connects to the WebSocket server hosted by the backend.
It starts generating random speed data every second, which is sent over WebSocket to the backend.
The React app updates the chart in Real-time based on the received data.

- **Backend:**

The backend listens for incoming WebSocket connections.
When it receives data from a client (React app), it stores the data in the MySQL database and sends the same data back to the sender via WebSocket.

- **Database:**

Each speed data received from the Frontend is stored with a timestamp for persistence.

![Web flow](https://github.com/user-attachments/assets/42afeb68-40c1-479e-bc53-ad7288ed5627)



## Explanation of the Flow
- **Frontend (React App):**
The React app initializes a WebSocket connection to the backend server at ws://localhost:8765.
It starts generating speed data randomly every second and sends the data as a WebSocket message.
Upon receiving the message from the backend (same data sent back), it updates the chart in real-time with new speed values.

- ** Backend (Flask & WebSocket):**
The Flask app exposes a WebSocket endpoint and accepts connections from the React frontend.
For each WebSocket connection, it stores the connection in a dictionary (by connection ID).
When data is received from the frontend, the backend stores this data into MySQL and immediately sends the same data back to the frontend, ensuring that the sender gets the same data that was sent.

- ** Database (MySQL): - **
Each time the backend receives speed data, it stores the speed and timestamp into the MySQL database using the following SQL query:
** SQL
  
Copy code
INSERT INTO speed_data (speed, timestamp) VALUES (%s, %s);


![HLL Diagram](https://github.com/user-attachments/assets/f8a7009b-f2f8-4f79-a932-09f1af86c32e)


## Backend API
- WebSocket API (ws://localhost:8765)
- The backend WebSocket server listens for connections at ws://localhost:8765. Each connection is assigned a unique ID.

Message Format:
The frontend sends data in the following format:

-- JSON
## {
  ## "speed": <speed_value>,
##   "timestamp": <current_time>
## }

Action on Data:
Upon receiving the data, the backend stores it in the MySQL database and sends the same data back to the sender.



## HTTP API (POST http://localhost:8765/send)
- The backend also provides an HTTP endpoint to send speed data to specific WebSocket connections. This API can be used for debugging or if you need to send data from other sources.

- ## {
  ## "connection_id": <connection_id>,
  ## "speed": <speed_value>,
  ## "timestamp": <current_time>
## } 

## Challenges Addressed:

- Real-time data flow between client and server.

- Persistent storage of data for future analysis.

- Scalability and environment consistency with Docker.

## Opportunities Exploited:

- Utilizing WebSockets for low-latency communication.

- Leveraging MySQL for robust data management.

- Streamlining deployment with Docker.


## CONCLUSION:
This project demonstrates a simple speedometer system using React for the frontend, Flask for the backend with WebSocket support, and MySQL for persistent data storage. The WebSocket connection allows real-time data communication between the frontend and backend, while MySQL stores the speed data with timestamps for future reference.
  







