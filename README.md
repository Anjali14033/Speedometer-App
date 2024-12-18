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













## Technologies Used

- **Streamlit:** For creating the web application interface.
- **Google Generative AI (Gemini Pro Vision):** For processing and analyzing the resume content.
- **Python:** The primary programming language used for backend development.
- **PYPDF2:** #Python package that allows you to work with PDF files.
            - #It provides functionalities for reading, manipulating, and extracting information from PDF documents


---


