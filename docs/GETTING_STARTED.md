# 🚀 Getting Started with SpeakFlow

> **Prerequisites**
> *   **Node.js v18+**
> *   **Modern Browser** (Chrome/Edge/Safari)
> *   **Microphone**

## 1. Environment Setup

The app is **Zero-Config**. No API keys or backend servers are required because it runs entirely in the browser.

---

## 2. Installation & Launch

### Step 1: Clone & Install
```bash
git clone https://github.com/Kimosabey/speak-flow.git
cd speak-flow
npm install
```

### Step 2: Start Client
```bash
npm run dev
# Running at http://localhost:5173
```

> **Mobile Testing Note**:
> Browsers block Microphone access on HTTP (unless it's localhost).
> To test on mobile, use **ngrok** or **Vite's --host** flag with a self-signed cert.

---

## 3. Usage Guide

1.  **Grant Permissions**: Click "Allow" when the browser asks for Microphone access.
2.  **Calibrate**: Sit in a quiet room for 3 seconds while the "Noise Calibration" runs.
3.  **Practice**:
    *   Read the French word shown (e.g., "Février").
    *   Speak clearly into the mic.
    *   Watch the feedback (Green/Orange/Red).

---

## 4. Running Tests

### Unit Tests
```bash
npm test
```

### Browser Compatibility Check
Open console (`F12`) and check for:
*   `[ASR] Service initialized`
*   `[VAD] Audio Context running`
