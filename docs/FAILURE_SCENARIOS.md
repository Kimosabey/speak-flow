# 🛡️ Failure Scenarios & Resilience

> "The Browser is a hostile environment. Audio can break at any time."

This document details how SpeakFlow handles hardware conflicts and OS restrictions.

## 1. Failure Matrix

| Component | Failure Mode | Impact | Recovery Strategy |
| :--- | :--- | :--- | :--- |
| **Microphone** | Permission Denied | **Critical**. App blocked. | **Visual Guide**. Show tailored instructions for unblocking mic in Chrome/Safari settings. |
| **ASR API** | "Network Error" | **Major**. No transcription. | **Retry Loop**. The ASR service auto-restarts the listening session up to 3 times before showing a "Check Connection" toast. |
| **iOS Safari** | Audio Context Suspended | **Minor**. No sound/viz. | **Touch-to-Resume**. iOS suspends audio until a user touches the screen. We attach a `resume()` listener to the first "Start" button click. |

---

## 2. Deep Dive: The "iOS 100vh" Bug

### The Problem
On mobile Safari, the bottom toolbar floats *over* the viewport. Setting `height: 100vh` causes the "Next" button to be hidden behind the browser UI.

### The Solution: `dvh` Units
We use Dynamic Viewport Height (`100dvh`) in our Chakra UI theme.
```css
/* ensuring the app always fits the visible area */
.app-container {
  height: 100dvh;
  overflow: hidden;
}
```

---

## 3. Resilience Testing

### Test 1: The "Mute" switch
1.  Hardware mute your microphone.
2.  Try to speak.
3.  **Expectation**: The "Noise Floor" detector will trigger a "We can't hear you" tooltip after 3 seconds of silence.

### Test 2: Background Noise
1.  Play loud music.
2.  Refresh the page (Calibration runs).
3.  **Expectation**: The noise floor rises to ignore the music. You must speak *louder* than the music to trigger the VAD.
