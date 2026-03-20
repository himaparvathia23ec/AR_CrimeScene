🧠 AR/VR Crime Scene Memory Distortion Simulator
An AI-powered AR/VR application designed to analyze how human memory can be distorted during crime scene observation using immersive environments and cognitive analysis.
🚀 Overview
This project simulates a 3D crime scene where users observe details and later answer recall questions. The system analyzes their responses to measure:
* Memory Accuracy
* Suggestibility (false memories)
* Memory Stability
It combines AR/VR, AI-based analysis, and backend systems to create a realistic and research-oriented experience.
🎯 Problem Statement
Human memory is not always reliable, especially in high-stress situations like crime scenes. Eyewitnesses may:
* Forget details
* Recall incorrect information
* Be influenced by misleading cues
This project aims to quantify and analyze memory distortion.
💡 Solution
We built an interactive system that:
1. Displays a 3D crime scene (Unity)
2. Allows users to explore using phone movement (gyroscope)
3. Introduces a distraction task
4. Collects recall responses
5. Uses AI logic to analyze memory distortion
6. Generates a Memory Stability Report
🏗️ Tech Stack
Frontend
* Unity (AR/VR Simulation)
* Gyroscope-based camera interaction
Backend
* FastAPI (Python)
* MongoDB (Database)
AI / Analysis
* Rule-based memory analysis
* Fuzzy matching & synonym detection
* Confidence & response-time weighting
⚙️ System Architecture

```
Unity (Crime Scene)
        ↓
User Recall Responses
        ↓
FastAPI Backend
        ↓
MongoDB Database
        ↓
AI Analyzer
        ↓
Memory Stability Report
        ↓
Dashboard / Output
```

🔄 Workflow
1. User starts experiment
2. Observes crime scene (25 seconds)
3. Completes a distraction task
4. Views modified scene
5. Answers recall questions
6. Backend analyzes responses
7. System generates memory report
📊 Key Metrics
* Accuracy Score `correct answers / total questions`
* Suggestibility Index `false memories / total questions`
* Memory Stability
   * Low
   * Moderate
   * High
📁 Project Structure

```
AR_CrimeScene_MemoryTest
├── backend
│   ├── api
│   ├── ai
│   ├── database
│   ├── models
│   └── main.py
│
├── Crime scene 1 (Unity)
│   ├── Assets
│   ├── Scenes
│   └── Scripts
│
├── dashboard (optional)
└── README.md
```

▶️ How to Run
1. Setup Backend

```
cd backend
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
uvicorn main:app --reload
```

Open:

```
http://127.0.0.1:8000/docs
```

2. Run Unity
* Open project in Unity
* Run the scene
* Ensure API URL is connected to backend
📌 Features
* Immersive AR/VR crime scene simulation
* Gyroscope-based navigation
* AI-based memory distortion detection
* Real-time performance optimization
* End-to-end system (Frontend + Backend + AI)
🔮 Future Improvements
* Full AR integration using camera
* Attention heatmaps (user focus tracking)
* Machine learning-based prediction
* Multi-user experiments
* Advanced dashboard visualization
👥 Team
* Hima
* Harini
* Harshita
* Chandana
🏁 Conclusion
This project demonstrates how AI + AR/VR can be used to study human cognitive behavior, especially in critical domains like crime investigation and forensic psychology.
