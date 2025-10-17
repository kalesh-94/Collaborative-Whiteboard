# 🖊️ Collaborative Whiteboard

A real-time collaborative whiteboard app built using the MERN stack and Socket.IO, allowing multiple users to draw together and share their cursors instantly — no login required!  
Just create or join a room with a code and start collaborating live.

## 🚀 Overview

This application enables users to draw simultaneously on a shared canvas.  
Anyone can join by entering a room code — no authentication needed.  
All drawings, strokes, and cursor movements are updated live across every connected user in the same room.

## ⚙️ Tech Stack
| Layer | Technology |
|--------|-------------|
| Frontend | React.js |
| Backend | Node.js + Express |
| Database | MongoDB |
| Real-time | Socket.IO |
| Styling | Tailwind CSS / CSS |

## ✨ Key Features

### 🧩 Room Management
- Join rooms using a 6–8 character alphanumeric code  
- No login or signup process  
- If a room doesn’t exist, it’s automatically created  

### 🖍️ Drawing Tools
- Pencil tool with multiple color options (black, red, blue, green)  
- Adjustable stroke width via slider  
- Clear canvas option  
- Smooth line drawing using HTML5 Canvas  

### ⚡ Real-time Collaboration
- Live drawing synchronization across all users  
- Cursor sharing with unique user colors  
- Real-time user count displayed per room  
- Multi-tab synchronization  

## 🗂️ Folder Structure
```
project-root/
├── client/               # React frontend
│   ├── src/
│   │   ├── components/
│   │   │   ├── RoomJoin.jsx
│   │   │   ├── Whiteboard.jsx
│   │   │   ├── DrawingCanvas.jsx
│   │   │   ├── Toolbar.jsx
│   │   │   └── UserCursors.jsx
│   │   ├── socket.js
│   │   └── App.js
│   └── package.json
│
├── server/               # Express + Socket.IO backend
│   ├── models/
│   │   └── Room.js
│   ├── routes/
│   │   └── roomRoutes.js
│   ├── socket/
│   │   └── socketHandlers.js
│   ├── server.js
│   └── package.json
│
├── README.md
```

## ⚙️ Setup Instructions

### 🧰 Prerequisites
- Node.js (v16 or later)
- MongoDB (local or MongoDB Atlas)
- npm or yarn

### 🔧 Installation

#### 1️⃣ Clone the Repository
```bash
git clone https://github.com/your-username/collaborative-whiteboard.git
cd collaborative-whiteboard
```

#### 2️⃣ Backend Setup
```bash
cd server
npm install
```
Create a `.env` file inside the `server/` folder:
```
PORT=8000
MONGODB_URI=your_mongodb_connection_string
```

#### 3️⃣ Frontend Setup
```bash
cd ../client
npm install
```
Create a `.env` file inside the `client/` folder:
```
VITE_BACKEND_URL=http://localhost:8000
```

#### ▶️ Start the Frontend
```bash
npm run dev
```

## 📡 API Endpoints
| Method | Endpoint | Description |
|---------|-----------|-------------|
| POST | /api/rooms/join | Join or create a room |
| GET | /api/rooms/:roomId | Fetch room details |

**Example POST Request:**
```http
POST /api/rooms/join
Content-Type: application/json

{
  "roomId": "abc123"
}
```

## 🔌 Socket.IO Events

### Client → Server
- `join-room` — join a room by ID  
- `cursor-move` — send live mouse position  
- `draw-start` — begin a drawing stroke  
- `draw-move` — continue the stroke  
- `draw-end` — finish drawing  
- `clear-canvas` — clear canvas for everyone  

### Server → Client
- `user-count` — update active user count  
- `cursor-update` — share other users’ cursor positions  
- `draw-start` — broadcast stroke start  
- `draw-move` — broadcast ongoing strokes  
- `draw-end` — broadcast end of stroke  
- `clear-canvas` — clear all users’ canvases  

## 🧠 Architecture Overview
```
[Client Browser]
   ↓ Socket.IO
[React App - Frontend]
   ↓ API & WebSocket
[Express Server - Backend]
   ↓
[MongoDB Database]
```

## 🚀 Deployment Guide

### 1️⃣ Backend Deployment
Use platforms like:
- Render
- Railway
- Vercel (Serverless)
- VPS / Docker

Make sure:
- WebSockets are enabled (`transports: ['websocket']`)
- CORS is configured properly
- MongoDB URI (Atlas recommended) is added to environment variables

**Example production `.env`:**
```
PORT=8000
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/whiteboard
```

### 2️⃣ Frontend Deployment
Use:
- Vercel
- Netlify

Set:
```
VITE_BACKEND_URL=https://your-backend-url.com
```

### 3️⃣ MongoDB Atlas Setup
- Create a cluster on MongoDB Atlas  
- Whitelist your backend IP or allow access from anywhere  
- Replace your local MongoDB URI with the Atlas connection string
