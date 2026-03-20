<div align="center">

# 🥽 AR/VR Crime Scene Memory Distortion Simulator

### *Can you trust your own memory?*

![Unity](https://img.shields.io/badge/Unity-AR%2FVR-black?style=for-the-badge&logo=unity&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-Python-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-Database-47A248?style=for-the-badge&logo=mongodb&logoColor=white)
![AI](https://img.shields.io/badge/AI-Memory%20Analysis-blueviolet?style=for-the-badge&logo=openai&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

<br/>

> **An immersive AI-powered application that places you inside a 3D crime scene —**
> **then scientifically measures how accurately your memory holds up.**

<br/>

```
 ██████╗██████╗ ██╗███╗   ███╗███████╗    ███████╗ ██████╗███████╗███╗   ██╗███████╗
██╔════╝██╔══██╗██║████╗ ████║██╔════╝    ██╔════╝██╔════╝██╔════╝████╗  ██║██╔════╝
██║     ██████╔╝██║██╔████╔██║█████╗      ███████╗██║     █████╗  ██╔██╗ ██║█████╗  
██║     ██╔══██╗██║██║╚██╔╝██║██╔══╝      ╚════██║██║     ██╔══╝  ██║╚██╗██║██╔══╝  
╚██████╗██║  ██║██║██║ ╚═╝ ██║███████╗    ███████║╚██████╗███████╗██║ ╚████║███████╗
 ╚═════╝╚═╝  ╚═╝╚═╝╚═╝     ╚═╝╚══════╝    ╚══════╝ ╚═════╝╚══════╝╚═╝  ╚═══╝╚══════╝
```

</div>

---

## 🧠 What Is This?

Human memory is **not a recording** — it's a reconstruction. Under stress, people forget details, fabricate information, and are easily influenced by misleading cues.

This project **quantifies that distortion** by placing users inside an immersive 3D crime scene and measuring three cognitive dimensions:

| Metric | Formula | What It Means |
|--------|---------|---------------|
| 🎯 **Memory Accuracy** | `correct answers / total questions` | How much you actually remembered |
| 🌀 **Suggestibility Index** | `false memories / total questions` | How easily your memory was influenced |
| 🧩 **Memory Stability** | `Low · Moderate · High` | Overall reliability of your recall |

---

## 🚀 Demo Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   👁️  Observe Scene        🧩 Distraction Task                  │
│   [ 25 seconds ]    ──►   [ cognitive load ]                   │
│                                                                 │
│   🔄 Modified Scene        📝 Recall Questions                  │
│   [ altered details ] ──► [ answer under pressure ]            │
│                                                                 │
│   🤖 AI Analysis           📊 Memory Report                     │
│   [ fuzzy match + NLP ] ─► [ accuracy · suggestibility ]       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🏗️ System Architecture

```
                        ┌──────────────────────┐
                        │   🎮  Unity Client    │
                        │  (AR/VR Crime Scene)  │
                        │  Gyroscope Navigation │
                        └──────────┬───────────┘
                                   │  HTTP / REST
                        ┌──────────▼───────────┐
                        │   ⚡  FastAPI Backend  │
                        │   main.py  ·  api/    │
                        └────┬──────────┬───────┘
                             │          │
               ┌─────────────▼──┐  ┌───▼──────────────┐
               │ 🗄️  MongoDB    │  │  🤖  AI Analyser  │
               │   (sessions,   │  │  fuzzy match      │
               │    responses)  │  │  synonym detect   │
               └────────────────┘  │  confidence wt.   │
                                   └───────┬───────────┘
                                           │
                        ┌──────────────────▼───────────┐
                        │   📊  Memory Stability Report │
                        │   Accuracy · Suggestibility  │
                        └──────────────────────────────┘
```

---

## 💡 Features

- 🥽 **Immersive AR/VR Crime Scene** — fully navigable 3D environment in Unity
- 📱 **Gyroscope-based Camera** — explore the scene using phone movement
- 🧩 **Distraction Task Engine** — induces natural memory interference
- 🔄 **Scene Modification System** — introduces subtle suggestibility cues
- 🤖 **AI Memory Analyser** — rule-based engine with fuzzy matching & synonym detection
- ⏱️ **Response-time Weighting** — confidence scores factor in answer hesitation
- 📊 **Automated Report Generation** — Memory Stability Report per session
- 🗄️ **Persistent Storage** — MongoDB stores all sessions for research analysis

---

## 🛠️ Tech Stack

### Frontend
![Unity](https://img.shields.io/badge/Unity-000000?style=flat-square&logo=unity&logoColor=white)
![C#](https://img.shields.io/badge/C%23-239120?style=flat-square&logo=csharp&logoColor=white)

- **Unity** — AR/VR 3D crime scene simulation
- **Gyroscope API** — phone-based camera navigation

### Backend
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white)

- **FastAPI** — high-performance REST API
- **MongoDB** — session & response storage

### AI / Analysis
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)

- **Rule-based memory analysis engine**
- **Fuzzy string matching** — handles typos & partial recalls
- **Synonym detection** — semantically equivalent answers accepted
- **Confidence + response-time weighting**

---

## 📁 Project Structure

```
AR_CrimeScene_MemoryTest/
│
├── 📂 backend/
│   ├── api/              # Route handlers & endpoints
│   ├── ai/               # Memory analysis engine
│   ├── database/         # MongoDB connection & helpers
│   ├── models/           # Pydantic data schemas
│   └── main.py           # FastAPI entry point
│
├── 📂 CrimeScene1/       # Unity Project
│   ├── Assets/
│   ├── Scenes/
│   └── Scripts/
│
├── 📂 dashboard/         # Optional visualisation layer
└── README.md
```

---

## ⚙️ Getting Started

### Prerequisites

- Python 3.9+
- Unity 2022+
- MongoDB (local or Atlas)

### 1️⃣ Backend Setup

```bash
# Clone the repository
git clone https://github.com/your-username/AR_CrimeScene_MemoryTest.git
cd AR_CrimeScene_MemoryTest/backend

# Create virtual environment
python -m venv .venv

# Activate (Windows)
.\.venv\Scripts\activate

# Activate (macOS/Linux)
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Start the server
uvicorn main:app --reload
```

📡 API docs auto-generated at: `http://127.0.0.1:8000/docs`

### 2️⃣ Unity Setup

```
1. Open Unity Hub → Add Project → select /CrimeScene1/
2. Open the main crime scene in Scenes/
3. In the API Config, set base URL → http://127.0.0.1:8000
4. Press ▶ Play to start simulation
```

---

## 🔬 How Memory Analysis Works

```python
# Simplified analysis pipeline
def analyse_response(user_answer, correct_answer, response_time):
    
    # Step 1: Exact match
    if user_answer == correct_answer:
        return score(1.0)
    
    # Step 2: Fuzzy match (handles typos)
    if fuzzy_ratio(user_answer, correct_answer) > 0.85:
        return score(0.9)
    
    # Step 3: Synonym detection
    if are_synonyms(user_answer, correct_answer):
        return score(0.8)
    
    # Step 4: Apply response-time confidence weight
    confidence = 1.0 - (response_time / MAX_TIME)
    return score(0.0, confidence_penalty=confidence)
```

---

## 🔮 Roadmap

- [x] 3D crime scene with gyroscope navigation
- [x] Distraction task & scene modification
- [x] AI-based memory analysis engine
- [x] Memory Stability Report generation
- [ ] 📸 Full AR mode using live camera feed
- [ ] 🔥 Attention heatmaps (gaze & focus tracking)
- [ ] 🤖 ML-based prediction models (LSTM / transformer)
- [ ] 👥 Multi-user concurrent experiment support
- [ ] 📊 Advanced longitudinal dashboard

---

## 👥 Team

| Member | Role |
|--------|------|
| 👩‍💻 **Hima** | AR/VR Development |
| 👩‍💻 **Harini** | Backend & API |
| 👩‍💻 **Harshita** | AI Analysis Engine |
| 👩‍💻 **Chandana** | Database & Integration |

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

### 🧠 *"Memory is not what happened. It's what you think happened."*

**Built with ❤️ using Unity · FastAPI · MongoDB · AI**

⭐ Star this repo if you find it interesting!

</div>
