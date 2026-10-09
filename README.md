# MAX AI — Your Personal Futuristic AI Assistant

MAX AI is a premium, futuristic Android personal assistant application inspired by JARVIS and Google Gemini. Built natively with **Kotlin** and **Jetpack Compose**, MAX AI combines natural language reasoning, live voice conversations, image understanding, persistent conversation history, user-controlled AI memory, and smart device actions.

---

## 🌟 Implemented Features

### 1. Dual-Mode Voice Interaction
- **Official Gemini Live API (Bidirectional Audio Streaming)**:
  - Real-time bidirectional WebSocket session via `BidiGenerateContent` (`wss://generativelanguage.googleapis.com/ws/google.ai.generativelanguage.v1beta.GenerativeService.BidiGenerateContent`).
  - Low-latency 16kHz PCM microphone capture via `AudioRecord` streamed as Base64 `realtimeInput` chunks.
  - Native 24kHz PCM audio playback streaming via `AudioTrack`.
  - Seamless barge-in / interruption handling: users can speak over MAX or tap the "Interrupt MAX" control to instantly flush audio playback and take the conversational floor.
  - Prebuilt voice personas: Aoede (Warm & Expressive), Puck (Upbeat), Charon (Calm & Resonant), Kore, and Fenrir.
- **Mode A: Quick Voice Input & Spoken Responses (Fallback)**:
  - Speech recognition using Android `SpeechRecognizer` and spoken answers via Android `TextToSpeech` (TTS).

### 2. Multi-turn Google Gemini AI Engine
- Integrated with modern Gemini models (`gemini-3.5-flash`, `gemini-3.8-flash`, and `gemini-3.1-pro-preview`).
- Real-time Server-Sent Events (SSE) streaming responses.
- Multimodal image reasoning (attach photos or diagrams from the gallery to ask visual questions or transcribe math/code).
- Google Search Grounding toggle for up-to-date web answers with citations.
- Structured persona: Courteous, humble, precise, and supportive.

### 3. Specialized Assistant Modes
- **General Assistant Mode**: Everyday questions, tasks, productivity, and ideas.
- **Coding Mode**: Software engineering specialist. Renders clean code blocks with syntax styling, language badges, and a 1-tap **Copy Code** button.
- **Study Mode**: Socratic educator. Breaks down complex topics step-by-step and asks check-for-understanding practice questions.

### 4. Smart Android Phone Actions
Allowlisted device actions with explicit confirmation dialogs for sensitive intents:
- Open apps: YouTube, Camera, Google Maps, Chrome, Calculator, Calendar, Clock.
- Open Android Settings: Wi-Fi, Bluetooth, Display, Sound, and System settings.
- Prepare Phone Calls: Uses safe `ACTION_DIAL` with user pre-confirmation dialog before launching the dialer.
- Prepare SMS Messages: Prepares SMS draft with message body and confirmation dialog.
- Navigation: Direct Google Maps search intents.
- Web navigation: Safe browser URLs.

### 5. Persistent Conversation History (Room Database)
- Fully private on-device SQLite database via Android Room.
- Automatic conversation title generation.
- Search past conversations in real-time.
- Rename, delete individual chats, or clear entire history.

### 6. User-Controlled AI Memory
- Independent memory store where users can inspect what MAX remembers.
- Enable/disable toggle switch.
- Add custom preferences (e.g., "I prefer Kotlin coroutine examples", "I study physics").
- Injected automatically into the system instructions for personalized cross-session responses.

### 7. Custom UI/UX Design System
- Futuristic Dark Theme (Deep Midnight `#070A13`, Dark Navy `#0F172A`, Electric Blue `#38BDF8`, Cyber Violet `#818CF8`, Neon Cyan `#22D3EE`).
- High-efficiency custom animated vector adaptive launcher icon (`ic_launcher`).
- Material 3 edge-to-edge support with dynamic keyboard insets.

---

## 🔑 Gemini API Key Configuration

1. In Google AI Studio, open the **Secrets** panel.
2. Add a new secret named `GEMINI_API_KEY` and paste your Google Gemini API key.
3. The applet automatically injects this secret into `BuildConfig.GEMINI_API_KEY` at build time.

---

## 🛠️ Build and Testing Instructions

### Run Unit Tests
```bash
gradle :app:testDebugUnitTest
```

### Build Debug APK
```bash
gradle :app:assembleDebug
```
The compiled APK will be located at:
`app/build/outputs/apk/debug/app-debug.apk`

---

## 📱 Permissions Declared in AndroidManifest.xml
- `android.permission.INTERNET`: Required for Gemini API calls.
- `android.permission.ACCESS_NETWORK_STATE`: Network availability checks.
- `android.permission.RECORD_AUDIO`: Microphone access for speech recognition and live voice interaction.
- `android.permission.VIBRATE`: Haptic feedback during interaction.
