# Basic Chat Application

## Overview
This is a backend application for a basic chat system, built as part of the Backend Beginner Level Assignment No. 3. It supports real-time messaging between users, allowing them to initiate chats, send and receive messages, and view message history. The application uses WebSockets for real-time communication and MongoDB for persistent message storage.

## Features
- Real-time messaging between users using WebSockets.
- Send and receive messages instantly.
- View message history between two users.
- Persistent storage of messages in MongoDB.

## Tech Stack
- **Backend Framework**: Express.js
- **Runtime**: Node.js
- **Database**: MongoDB
- **Real-time Communication**: Socket.IO (WebSocket implementation)

## Prerequisites
- Node.js (v24.2.0 or later recommended)
- MongoDB (local installation or MongoDB Atlas)
- npm (Node Package Manager)
- A browser to test the frontend (`index.html`)

## Project Structure
```
chat-app/
├── models/
│   └── Message.js    # Mongoose schema for messages
├── .env              # Environment variables
├── server.js         # Main server file
├── index.html        # Simple frontend for testing
├── package.json      # Project dependencies and scripts
└── README.md         # Project documentation
```

## Setup Instructions

### 1. Clone or Download the Project
If you haven't already, place the project files in a directory:
```bash
mkdir chat-app
cd chat-app
```

### 2. Install Dependencies
Install the required npm packages:
```bash
npm install
```

This will install the following dependencies:
- `express`
- `mongoose`
- `socket.io`
- `cors`
- `dotenv`

### 3. Set Up Environment Variables
Create a `.env` file in the root directory with the following content:
```
PORT=5002
MONGO_URI=mongodb://127.0.0.1:27017/chat-app
```

- `PORT`: The port where the server will run (set to 5002 as per your setup).
- `MONGO_URI`: The MongoDB connection string. If using MongoDB Atlas, replace this with your Atlas connection string (e.g., `mongodb+srv://<username>:<password>@cluster0.mongodb.net/chat-app`).

### 4. Start MongoDB
Ensure MongoDB is running on your machine:
- If using a local MongoDB instance:
  ```bash
  brew services start mongodb-community
  ```
  Or run manually:
  ```bash
  mongod
  ```
- Verify MongoDB is running on port `27017`:
  ```bash
  lsof -i :27017
  ```
- If using MongoDB Atlas, ensure your cluster is active and the `MONGO_URI` is correctly set in the `.env` file.

### 5. Start the Server
Run the server:
```bash
node server.js
```

You should see:
```
Server running on port 5002
MongoDB connected
```

If you encounter an `EADDRINUSE` error, the port `5002` is in use. Find the process using the port and terminate it:
```bash
lsof -i :5002
kill -9 <PID>
```

## Usage

### Test the API
- **Root Route**:  
  Confirm the server is running by visiting:  
  `http://localhost:5002`  
  Response: `Welcome to the Chat API! Use /messages/:sender/:receiver to get message history.`

- **Get Message History**:  
  Retrieve the message history between two users:  
  Example: `http://localhost:5002/messages/user1/user2`  
  Use `curl` to test:  
  ```bash
  curl http://localhost:5002/messages/user1/user2
  ```

### Test Real-Time Messaging
A simple frontend (`index.html`) is provided to test the chat functionality:
1. Open `index.html` in two browser tabs (or two different browsers/devices):
   - Tab 1: Set Sender as `user1`, Receiver as `user2`.
   - Tab 2: Set Sender as `user2`, Receiver as `user1`.
2. Send messages back and forth. Messages should appear in real-time in both tabs.
3. The message history will load automatically when you set the sender and receiver IDs.

### API Endpoints
The server runs on `http://localhost:5002`. Below are the available endpoints:

- **GET /**  
  Root route to confirm the server is running.  
  Response: `Welcome to the Chat API! Use /messages/:sender/:receiver to get message history.`

- **GET /messages/:sender/:receiver**  
  Retrieve message history between two users.  
  Example: `http://localhost:5002/messages/user1/user2`  
  Response: Array of messages (e.g., `[{"sender":"user1","receiver":"user2","content":"Hello!","timestamp":"2025-06-17T03:55:00.000Z"}]`.

### WebSocket Events (Used by the Frontend)
- **join_room**: Join a chat room based on sender and receiver IDs (e.g., `user1-user2`).
- **send_message**: Send a message to a specific room.
- **receive_message**: Receive a message in real-time from the room.

## Troubleshooting
- **MongoDB Connection Error**:
  - Ensure MongoDB is running on `127.0.0.1:27017`.
  - Check MongoDB logs: `cat /usr/local/var/log/mongodb/mongo.log`.
  - If local MongoDB fails, use MongoDB Atlas (see setup instructions above).
- **Port Conflict**:
  - Check if port `5002` is in use: `lsof -i :5002`.
  - Kill the process or change the `PORT` in `.env` if needed.
- **Infinite Loading in Browser**:
  - Test with `curl` to bypass browser issues: `curl http://localhost:5002`.
  - Ensure MongoDB is connected to avoid hanging on database queries.
  - Clear browser cache or try a different browser.

## License
This project is for educational purposes as part of the Backend Beginner Level Assignment No. 3.