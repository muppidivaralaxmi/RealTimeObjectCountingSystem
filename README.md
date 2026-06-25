# 🎯 Real-Time Object Counting System
### Built with Python (Flask) + YOLOv8 + HTML/JS Dashboard

---

## 📁 Project Structure
```
project/
├── backend/
│   ├── app.py              ← Main Python backend server
│   └── requirements.txt    ← Python packages to install
└── frontend/
    └── index.html          ← Dashboard webpage (open in browser)
```

---

## 🚀 HOW TO RUN (Step by Step)

### STEP 1 — Install Python
Download Python 3.10+ from: https://python.org/downloads
✅ Check "Add Python to PATH" during install

---

### STEP 2 — Install Required Packages
Open a terminal (Command Prompt on Windows) and run:
```bash
cd backend
pip install -r requirements.txt
```

This installs:
- Flask       → Web server
- OpenCV      → Camera access
- YOLOv8      → Object detection AI
- openpyxl    → Excel export

---

### STEP 3 — Start the Backend Server
```bash
cd backend
python app.py
```

You should see:
```
✅ Database ready
🚀 Starting Object Counting Backend Server...
```

Leave this terminal open! (It's your server running)

---

### STEP 4 — Open the Dashboard
Open the file `frontend/index.html` in your browser.
(Just double-click it, or drag it into Chrome/Firefox)

---

### STEP 5 — Connect a Camera

**Option A: IP Camera (phone or CCTV)**
- Install "IP Webcam" app on Android
- Connect phone and laptop to same WiFi
- Open the app, tap "Start server"
- In dashboard, enter: `http://192.168.x.x:8080/video`
- Click Start ▶

**Option B: Laptop webcam**
- In dashboard, enter: `0`
- Click Start ▶

**Option C: Simulation (for testing, no camera needed)**
- Leave the URL box blank
- Click Start ▶
- Fake detections will appear every few seconds

---

## 💡 How It Works (Line Crossing Logic)

```
Camera frame:
┌────────────────────────────┐
│                            │
│   [Car] moving down ↓      │
│                            │
│ ─ ─ ─ COUNTING LINE ─ ─ ─ │  ← When car crosses this line → COUNT!
│                            │
│                            │
└────────────────────────────┘
```

1. YOLO detects objects in each frame
2. Each object gets a unique tracking ID
3. We remember where each object was in the previous frame
4. If it moved from above the line to below → **COUNT IT!**
5. Each object is only counted ONCE (prevents double counting)

---

## 📊 Dashboard Features

| Feature | Description |
|---------|-------------|
| Live Camera | Real-time video with detection boxes |
| Live Counts | Updates every second automatically |
| People (M/F) | Separated male and female counts |
| Vehicles | Cars, Motorcycles, Trucks separately |
| Objects | Common items (cups, chairs, etc.) |
| Daily Report | Hourly bar chart + category pie chart |
| CSV Export | Download data as spreadsheet |
| Excel Export | Download as formatted .xlsx file |

---

## ❓ Common Problems

**"Cannot connect to backend"**
→ Make sure `python app.py` is running in another terminal

**"Camera won't open"**
→ Check the IP address is correct and phone/camera is on same WiFi

**"YOLO not installed"**
→ Run: `pip install ultralytics`

**"openpyxl not installed" (Excel export fails)**
→ Run: `pip install openpyxl`

---

## 🏫 How to Explain to Mentor

1. **Frontend** = `index.html` — the webpage dashboard
2. **Backend** = `app.py` — Python server that runs on your laptop
3. **Database** = `counts.db` — automatically created, stores all counts
4. **YOLO** = AI model that detects objects in camera frames
5. **Line Crossing** = When an object moves across the yellow line on screen → it gets counted

The frontend talks to the backend using simple HTTP requests (fetch API).
The backend sends the camera video as a stream of JPEG images.
