# 🧍 PostureAI

**Real-time posture detection and training — runs entirely in your browser. No server, no cloud, no installs.**

PostureAI uses your webcam + [MediaPipe Pose](https://ai.google.dev/edge/mediapipe/solutions/vision/pose_landmarker) to detect body pose landmarks, then trains a small neural network (via [TensorFlow.js](https://www.tensorflow.org/js)) to classify your posture into any labels you define. Everything — model training, inference, history, and settings — lives in your browser's `localStorage`.

🔗 **Live App:** [https://martmet.github.io/postureai/](https://martmet.github.io/postureai/)

---

## ✨ Features

- **Live pose detection** via MediaPipe Pose Landmarker (GPU-accelerated, no install)
- **Custom labels** — train on any posture categories you want (good, bad, slouched, leaning-left, …)
- **Per-label colours** — each label gets a unique colour used consistently across the UI, heatmap, and skeleton overlay
- **Auto-save / auto-load** — model and data persist across reloads automatically
- **Continuous Learning** — instantly correct the model by capturing samples during live prediction to auto-retrain in the background
- **Live Probability HUD** — displays a dynamically sorted ranking of all custom label probabilities in real-time
- **Continuous Probability Heatmap** — 24 × 60 minute grid that mathematically blends your label colors across RGB channels based on exact prediction confidence
- **Health rings & score** — visual rings for upright time, consistency streak, and break frequency
- **Bad posture alert** — configurable timer alert (5 s–300 s) with escalating audio beeps; repeats until you sit up
- **Home Assistant webhook** — send posture state to HA on every change; no token required
- **Export / import** — save your training dataset as JSON and reload it later

---

---

## 🎓 How to train your model

1. Click **▶ Start Camera** and allow webcam access
2. Go to the **Collection** tab — add label names (defaults: `good`, `bad`)
3. Hold each posture and click its capture button to collect samples (aim for 30+ per label)
4. Switch to the **Training** tab and click **Start Training**
5. **Continuous Learning:** Once predicting, if the AI makes a mistake, simply click the correct label's capture button — the model will instantly learn and auto-retrain in the background!
6. The model saves automatically — it's ready next time you open the app

---

## 🔔 Bad Posture Alert

Found in the **Settings/Connectivity** area. Enable the checkbox and set a threshold (e.g. 30 s). Once your probability for good posture drops for that long, a beep fires. Each successive repeat escalates in pitch and number of pulses until good posture is resumed.

---

## 🏠 Home Assistant Integration

In the **Connectivity** tab:

1. In HA → **Settings → Automations → New → Trigger: Webhook** — copy the URL
2. Paste it into PostureAI and click **Save**
3. Use the **🧪 Test** button to verify the connection

PostureAI posts this JSON on every posture change:

```json
{
  "posture": "bad",
  "is_good": false,
  "elapsed_bad_s": 47,
  "stats": { "good": 312, "bad": 47 }
}
```

---

## 🗂 Project Structure

```
postureai/
└── index.html    # The entire app — HTML + CSS + JS, single file
```

---

## 🛠 Tech Stack

| Library | Purpose |
|---|---|
| [MediaPipe Tasks Vision](https://ai.google.dev/edge/mediapipe/solutions/vision/pose_landmarker) | Real-time pose landmark detection |
| [TensorFlow.js](https://www.tensorflow.org/js) | Neural network training & inference |

| Web Audio API | Alert beeps (no files needed) |
| Notifications API | Desktop posture alerts |

All loaded from CDN — no build step, no `npm install`.

---

## 📄 License

MIT — do whatever you want with it.
