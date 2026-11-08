##  LINKS
#### 🔗 Live Demo https://threat-detection-system.vercel.app
# 🛡️ Smart Threat Detection System

**Contibutions to the Project**
-**Team Lead** ~Siddhant Singh Katiyar (24155959) : Frontend & Backend
-Tanmay Upadhyay (241551009) : AI Model
-Swadhin Pradipta Das (241551008) : Database

Real-time AI threat detection system that identifies weapons, unattended bags, and persons with intelligent threat classification and instant alerts.

##  Features

- **YOLOv8 + ByteTrack**: Accurate object detection with persistent tracking across frames to prevent duplicate alerts
- **Smart Threat Levels**: Context-aware classification (SAFE, MEDIUM, HIGH, CRITICAL) based on object type and behavior
- **Unattended Bag Detection**: Automatic escalation from MEDIUM (25s) to HIGH (45s) to CRITICAL (60s+) when bags are left alone
- **Triple-Layer Duplicate Prevention**: AI tracking, backend validation, and database constraints ensure no duplicate detections
- **Real-time Updates**: WebSocket connections provide instant alerts and live dashboard updates

##  Tech Stack

**AI Detection**: Python with YOLOv8 for object detection, ByteTrack for multi-object tracking, OpenCV for image processing  
**Backend**: FastAPI for REST API, MongoDB for data storage, WebSockets for real-time communication  
**Frontend**: React with Vite for fast UI development, TailwindCSS for modern styling

##  Quick Start

### Prerequisites
- Python 3.8+
- Node.js 16+
- MongoDB 4.4+
- Webcam or IP camera

### Installation

```bash
# Clone repository
git clone <repository-url>
cd smart-threat-detection

# Backend setup
cd threat-bakend
python -m venv venv
venv\Scripts\Activate.ps1
pip install -r requirements.txt

# Frontend setup
cd ../threat-frontend
npm install

# Optional AI model setup
cd ../AI-MODEL
pip install -r requirements.txt
```

### Configuration

Create `threat-bakend/.env` by copying `.env.example`:
```env
MONGO_URI=mongodb://localhost:27017/
```
Make sure MongoDB is running if you want to store and query detections.

### Run

```bash
# Terminal 1: Start Backend
cd threat-bakend
venv\Scripts\Activate.ps1
python -m uvicorn main:app --reload --host 0.0.0.0 --port 8000

# Terminal 2: Start Frontend
cd threat-frontend
npm run dev

# Optional Terminal 3: Start AI Detection
cd AI-MODEL
python threat_detection.py
```

Access at: `http://localhost:5173`

## 🎯 Threat Levels

| Object | Condition | Level | Color |
|--------|-----------|-------|-------|
| Person | Always | SAFE | 🟢 |
| Objects | Always | SAFE | 🟢 |
| Weapon | Always | CRITICAL | 🔴 |
| Bag (Attended) | Person nearby | SAFE | 🟢 |
| Bag (Unattended) | 25-45s | MEDIUM | � |
| Bag (Unattended) | 45-60s | HIGH | � |
| Bag (Unattended) | 60s+ | CRITICAL | 🔴 |

## 📡 API Endpoints

- `POST /api/detect/upload` - Upload detection
- `GET /api/detect/history` - Get detection history
- `GET /api/detect/alerts` - Get recent alerts
- `GET /api/detections/stats` - Get statistics
- `GET /api/system/status` - System status
- `WS /ws/alerts` - WebSocket real-time alerts

## � Project Structure

```
├── AI-model/              # YOLOv8 detection system
├── threat-backend/        # FastAPI backend + MongoDB
├── threat-frontend/       # React UI
└── README.md
```

## 🔧 Configuration Options

Edit `AI-model/threat_detection.py`:
```python
CONF = 0.45              # Detection confidence
FRAME_SKIP = 2           # Process every Nth frame
CRITICAL_TIME = 60       # Bag unattended threshold (seconds)
JPEG_QUALITY = 95        # Image quality
MAX_DIMENSION = 320      # Max image size (px)
```

## 🧪 Testing

```bash
python test_alerts_endpoint.py      # Test alerts API
python test_duplicate_handling.py   # Test duplicate prevention
```

##  Performance Tips

- Use `yolov8n.pt` for faster detection (less accurate)
- Increase `FRAME_SKIP` for better performance
- Enable GPU with CUDA for PyTorch
- Use production build: `npm run build`

## 🔐 Security (Production)

- Enable MongoDB authentication
- Add JWT/OAuth2 for API endpoints
- Use HTTPS with SSL certificates
- Implement rate limiting
- Restrict CORS origins

##  License

MIT License

---

**Built for enhanced security**