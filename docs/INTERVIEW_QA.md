# 🎤 Interview Cheat Sheet: SpeakFlow

## 1. The Elevator Pitch (2 Minutes)

"SpeakFlow is a **Client-Side AI** application for language learning.
It leverages the browser's native **Web Audio API** and **Web Speech API** to build a 'Duolingo-style' pronunciation coach that runs 100% offline.
I built a custom **Voice Activity Detector (VAD)** logic that calibrates to the room's noise floor, ensuring the app knows *exactly* when you start and stop speaking, providing a near-zero latency experience without expensive cloud servers."

---

## 2. "Explain Like I'm 5" (The Teacher)

"Imagine a very strict French teacher.
*   **The Problem**: Cloud apps are like mailing a tape to France and waiting for a letter back. Too slow!
*   **My Solution**: I put the teacher inside the browser.
*   **How**: Your phone listens to the sound waves (VAD). When the waves look like speech, it checks the dictionary (ASR). If you say 'Bonjour' correctly, it gives you a gold star instantly."

---

## 3. Tough Technical Questions

### Q: Why Web Speech API instead of Whisper?
**A:** "For a pronunciation game, **Latency** is king.
*   **Whisper**: High accuracy, but requires sending audio blob -> Server -> Inference -> Response (2-3s).
*   **Web Speech**: Native to the OS. Returns partial results in <100ms.
*   **Trade-off**: Web Speech is less accurate for long sentences, but for single-word practice (e.g., 'Février'), it is perfect and free."

### Q: How do you handle React State with 60fps Audio?
**A:** "Performance bottleneck.
If I updated React State every time the microphone sample changed (60 times a second), the app would freeze.
**Solution**: I decoupled them.
1.  **Audio Engine**: Runs outside React in a `requestAnimationFrame` loop, mutating a Canvas Ref directly.
2.  **React**: Only updates when 'Speech Started' or 'Result Received' events fire.
This keeps the UI buttery smooth (60fps) while processing heavy audio data."

### Q: How does the Fuzzy Matching work?
**A:** "I use the **Levenshtein Distance** algorithm.
It calculates the minimum number of edits (inserts, deletes, substitutions) to turn the User's word into the Target word.
*   Target: 'Janvier'
*   User: 'Janvie' (Distance = 1) -> Score: 80% (Pass)
*   User: 'Banana' (Distance = 6) -> Score: 0% (Fail)"
