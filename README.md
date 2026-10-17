---
title: yolo
colorFrom: blue
colorTo: indigo
sdk: docker
---

<div align="center">

<h1>⚡ YOLO (You Only Look Once)</h1>
<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=22&duration=3000&pause=1000&color=3B82F6&center=true&vCenter=true&width=700&lines=Upload+Label+Studio+exports;Fine-tune+YOLO11+on+your+classes;Real-time+webcam+detection" alt="Typing SVG"/>

<br/>

[![Python](https://img.shields.io/badge/Python-3.10+-3b82f6?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-2.x-4f46e5?style=for-the-badge&logo=flask&logoColor=white)](https://flask.palletsprojects.com/)
[![Ultralytics](https://img.shields.io/badge/YOLO11-Ultralytics-ff6f00?style=for-the-badge&logo=pytorch&logoColor=white)](https://github.com/ultralytics/ultralytics)
[![Docker](https://img.shields.io/badge/Docker-Ready-3b82f6?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![GitHub](https://img.shields.io/badge/GitHub-yolo-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/mnoorchenar/yolo)
[![Status](https://img.shields.io/badge/Status-Active-22c55e?style=for-the-badge)](#)

<br/>

[![Live Demo](https://img.shields.io/badge/%E2%96%B6_Live_Demo-Hugging_Face_Space-ffcc00?style=for-the-badge&logo=huggingface&logoColor=black)](https://huggingface.co/spaces/mnoorchenar/yolo)
[![Source Code](https://img.shields.io/badge/Source_Code-GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/mnoorchenar/yolo)

<br/>

**⚡ YOLO Custom Trainer** — A full end-to-end object detection playground. Upload a Label Studio YOLO export (max 5 MB), fine-tune YOLO11 on your custom classes with live training progress, then run real-time webcam detection — all from the browser.

<br/>

---

</div>

## Table of Contents

- [Features](#-features)
- [Architecture](#️-architecture)
- [Getting Started](#-getting-started)
- [Docker Deployment](#-docker-deployment)
- [Dashboard Modules](#-dashboard-modules)
- [ML Models](#-ml-models)
- [Project Structure](#-project-structure)
- [Author](#-author)
- [Disclaimer](#️-disclaimer)
- [License](#-license)

---

## ✨ Features

<table>
  <tr>
    <td>📦 <b>Label Studio Integration</b></td>
    <td>Upload YOLO-format zip exports (max 5 MB); auto-parses classes.txt and builds data.yaml. Uploading a new dataset automatically replaces the previous one.</td>
  </tr>
  <tr>
    <td>🧠 <b>Live Fine-tuning</b></td>
    <td>Server-side YOLO11 training with SSE-streamed epoch metrics (loss, mAP50). Dataset is cleaned up from disk after training completes.</td>
  </tr>
  <tr>
    <td>📹 <b>Real-time Webcam Detection</b></td>
    <td>WebRTC → Flask pipeline; custom-trained classes detected live at ~8 FPS</td>
  </tr>
  <tr>
    <td>🖼 <b>Image Inference</b></td>
    <td>Drag-and-drop single image detection with annotated output and confidence scores</td>
  </tr>
  <tr>
    <td>🐳 <b>Containerized Deployment</b></td>
    <td>Docker-first architecture, cloud-ready and scalable</td>
  </tr>
</table>

---

## 🏗️ Architecture

```
┌──────────────────────────────────────────────────────────┐
│                  YOLO Custom Trainer                     │
│                                                          │
│  ┌────────────┐   ┌────────────┐   ┌─────────────────┐  │
│  │ Label      │──▶│  YOLO11    │──▶│  Flask API      │  │
│  │ Studio ZIP │   │  Training  │   │  (Blueprints)   │  │
│  └────────────┘   └────────────┘   └────────┬────────┘  │
│                                             │            │
│  ┌──────────────────────────────────────────▼─────────┐  │
│  │              Bootstrap 5 UI (dark)                 │  │
│  │  /upload   /train (SSE progress)  /detect (WebRTC) │  │
│  └────────────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────────┘
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- Docker & Docker Compose
- Git

### Local Installation

```bash
# 1. Clone the repository
git clone https://github.com/mnoorchenar/yolo.git
cd yolo

# 2. Create a virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Configure environment variables
cp .env.example .env

# 5. Run the application
python app.py
```

Open your browser at `http://localhost:7860` 🎉

---

## 🐳 Docker Deployment

```bash
# Build and run with Docker Compose
docker compose up --build

# Or build and run manually
docker build -t yolo-custom-trainer .
docker run -p 7860:7860 yolo-custom-trainer
```

---

## 📊 Dashboard Modules

| Module | Description | Status |
|--------|-------------|--------|
| 📦 Dataset Upload | Label Studio YOLO zip ingestion (5 MB limit), class auto-detection, replaces previous dataset | ✅ Live |
| ⚙️ Training Config | Epoch / imgsz / batch / model-size selector | ✅ Live |
| 📈 Live Progress | SSE-streamed epoch metrics and terminal log | ✅ Live |
| 🗑 Auto Cleanup | Dataset deleted from disk after training; only weights are kept | ✅ Live |
| 📹 Webcam Detect | WebRTC → Flask → YOLO11 → annotated frame pipeline | ✅ Live |
| 🖼 Image Detect | Single-image drag-and-drop inference with result overlay | ✅ Live |

---

## 🧠 ML Models

```python
# Models available in YOLO Custom Trainer
models = {
    "yolo11n": "Nano   — fastest, ~2.6M params, best for real-time on CPU",
    "yolo11s": "Small  — good balance of speed and accuracy",
    "yolo11m": "Medium — solid accuracy for most use cases",
    "yolo11l": "Large  — high accuracy, slower inference",
    "yolo11x": "XLarge — maximum accuracy, heaviest model",
}
```

---

## 📁 Project Structure

```
yolo/
│
├── 📂 routes/
│   ├── __init__.py
│   ├── detect.py
│   ├── train.py
│   └── upload.py
├── 📂 static/                    # CSS, JavaScript & assets
│   └── css/
├── 📂 templates/                 # HTML templates
│   ├── base.html
│   ├── detect.html
│   ├── index.html
│   ├── train.html
│   └── upload.html
├── 📂 utils/
│   ├── __init__.py
│   ├── dataset.py
│   └── model_manager.py
├── 📄 .env.example               # Environment variable template
├── 📄 Dockerfile                 # HF Spaces-ready container (port 7860)
├── 📄 app.py                     # Flask app factory (5 MB limit, 413 handler)
├── 📄 docker-compose.yml         # Local multi-service orchestration
└── 📄 requirements.txt           # Python dependencies
```

---

## 👨‍💻 Author

<div align="center">

<table>
<tr>
<td align="center" width="100%">

<img src="https://avatars.githubusercontent.com/mnoorchenar" width="120" style="border-radius:50%; border: 3px solid #4f46e5;" alt="Mohammad Noorchenarboo"/>

<h3>Mohammad Noorchenarboo</h3>

<code>Data Scientist</code> &nbsp;|&nbsp; <code>AI Researcher</code> &nbsp;|&nbsp; <code>Biostatistician</code>

📍 &nbsp;Ontario, Canada &nbsp;&nbsp; 📧 &nbsp;[mohammadnoorchenarboo@gmail.com](mailto:mohammadnoorchenarboo@gmail.com)

──────────────────────────────────────

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/mnoorchenar)&nbsp;
[![Personal Site](https://img.shields.io/badge/Website-mnoorchenar.github.io-4f46e5?style=for-the-badge&logo=githubpages&logoColor=white)](https://mnoorchenar.github.io/)&nbsp;
[![HuggingFace](https://img.shields.io/badge/HuggingFace-ffcc00?style=for-the-badge&logo=huggingface&logoColor=black)](https://huggingface.co/mnoorchenar)&nbsp;
[![Google Scholar](https://img.shields.io/badge/Scholar-4285F4?style=for-the-badge&logo=googlescholar&logoColor=white)](https://scholar.google.ca/citations?user=nn_Toq0AAAAJ&hl=en)&nbsp;
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/mnoorchenar)

</td>
</tr>
</table>

</div>

---

## ⚠️ Disclaimer

> [!WARNING]
> This project is developed strictly for educational and research purposes. All datasets are user-provided and are automatically deleted from the server after training. No data is stored persistently. This software is provided "as is" without warranty of any kind.

---

## 📜 License

> **© 2025–2026 Mohammad Noorchenarboo — All Rights Reserved (with Attribution Exception)**

| Use case | Allowed? |
|---|---|
| ✅ Using, referencing, or showcasing this project **with clear credit** to the author and a link to [mnoorchenar.github.io](https://mnoorchenar.github.io/) | **Yes** |
| ❌ Copying, reproducing, or redistributing the source code in **any format** without attribution | **Not acceptable** |
| ❌ Presenting this work as your own or removing author credits | **Not acceptable** |

If you use or reference this project, you must visibly credit:

> **Mohammad Noorchenarboo** — [mnoorchenar.github.io](https://mnoorchenar.github.io/)

For any other use, please contact the author directly.

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:3b82f6,100:4f46e5&height=120&section=footer&text=Made%20with%20%E2%9D%A4%EF%B8%8F%20by%20Mohammad%20Noorchenarboo&fontColor=ffffff&fontSize=18&fontAlignY=80" width="100%"/>

[![GitHub Stars](https://img.shields.io/github/stars/mnoorchenar/yolo?style=social)](https://github.com/mnoorchenar/yolo/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/mnoorchenar/yolo?style=social)](https://github.com/mnoorchenar/yolo/fork)

<sub>The name "YOLO (You Only Look Once)" is used purely for academic and research purposes. Any similarity to existing product names or trademarks is entirely coincidental. This project has no affiliation with any commercial entity.</sub>

</div>
