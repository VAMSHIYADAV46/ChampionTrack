# 🏆 ChampionTrack – MVP Project Package

---

## 1. MVP-Blueprint
**Contents:**
- **Project Name:** ChampionTrack  
- **Vision:** Democratize sports talent discovery and provide scientific, AI-powered athlete performance tracking for inclusive development.  
- **Tech Stack:**  
  - **Frontend:** React.js (with Context/Redux, Chart.js/Recharts for dashboards)  
  - **Backend:** Node.js + Express.js  
  - **Database:** MongoDB  
  - **ML/AI:** MediaPipe + TensorFlow Lite, PyTorch, OpenCV  
- **Roles:** Athlete, Coach  
- **Features:**  
  - Video uploads (drills)  
  - AI-powered performance analysis (posture, speed, stamina, reaction time)  
  - Coach dashboard (review & feedback)  
  - Athlete dashboard (progress tracking)  

---

## 2. Project-Requirements-Document (PRD)
**Functional requirements:**
- Athletes can register, log in, upload videos.  
- ML pipeline analyzes uploaded drills and returns metrics.  
- Coaches can view athletes, review performance, give feedback.  
- Dashboards: athlete progress charts, coach reports.  

**Non-functional requirements:**
- Scalability: 100+ simultaneous video uploads.  
- Latency: analysis within 30 seconds.  
- Security: JWT authentication, password hashing.  

**Success criteria:**
- Accurate detection of posture, repetition count, and timing.  
- Smooth dashboard experience.  

---

## 3. System-Architecture
**Overview:**
- **Frontend:** React app → REST API  
- **Backend:** Express API (auth, uploads, metrics retrieval)  
- **Database:** MongoDB (users, videos, metrics, reports)  
- **ML Pipeline:** OpenCV → MediaPipe → TensorFlow Lite → PyTorch → MongoDB  

**Diagram:**  
Athlete → React UI → Express API → ML Service → MongoDB  
Coach → React UI → Express API → MongoDB  

---

## 4. API-Specification
```yaml
paths:
  /auth/register:
    post:
      summary: Register user (athlete/coach)

  /auth/login:
    post:
      summary: Login with JWT

  /videos/upload:
    post:
      summary: Athlete uploads a training video

  /metrics/{videoId}:
    get:
      summary: Retrieve analysis results

  /coach/feedback:
    post:
      summary: Coach gives feedback to athlete

```

## 5. Database-Schema

### Users
`{ "_id": "", "name": "", "email": "", "role": "athlete|coach", "passwordHash": "" }`

### Videos
`{ "_id": "", "userId": "", "url": "", "uploadedAt": "" }`

### Metrics
`{ "videoId": "", "postureScore": 0, "speed": 0, "stamina": 0, "reactionTime": 0 }`

### Feedback
`{ "coachId": "", "athleteId": "", "videoId": "", "comments": "", "date": "" }`

---

## 6. Frontend-Component-Blueprint

- AuthPage (Login/Register)  
- AthleteDashboard  
- UploadVideo  
- ProgressCharts  
- CoachDashboard  
- AthleteList  
- ReviewPerformance  
- FeedbackForm  

---

## 7. Backend-Services-Blueprint

- `routes/auth.js` → Register/Login  
- `routes/videos.js` → Upload, fetch  
- `routes/metrics.js` → Get analysis results  
- `routes/feedback.js` → Coach feedback  
- `middleware/auth.js` → JWT validation  

---

## 8. ML-Pipeline

- **Input:** Athlete uploads video (MP4)  
- **Preprocessing:** OpenCV extracts frames  
- **Pose Detection:** MediaPipe finds keypoints  
- **Inference:** TensorFlow Lite checks posture, speed, reps  
- **Advanced Analysis:** PyTorch evaluates stamina & reaction time  
- **Output:** Metrics stored in MongoDB (linked to `videoId`)  

---

## 9. Dashboard-Design-Spec

### Athlete Dashboard
- Progress charts  
- Video history with scores  
- Coach feedback  

### Coach Dashboard
- Athlete list  
- Video review (with metrics overlay)  
- Feedback form  

---

## 10. User-Journey-Flows

**Athlete Flow:**  
Register → Upload drill → AI analysis → Dashboard → Coach feedback  

**Coach Flow:**  
Register → Assigned athletes → View drills + metrics → Give feedback  

---

## 11. Testing-Plan

- **Unit:** Auth, video upload, metrics calculation  
- **Integration:** React ↔ Express ↔ MongoDB ↔ ML pipeline  
- **ML Evaluation:** Compare AI vs. coach review  

---

## 12. Future-Roadmap

- Real-time video feedback  
- Team dashboards  
- Mobile app (React Native)  
- AI training recommendations  
