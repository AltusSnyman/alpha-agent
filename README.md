Alpha Agent
A Siri-like voice assistant app built with Expo SDK 53 and ElevenLabs Conversational AI. Alpha Agent provides natural two-way voice conversations through an intuitive mobile interface, leveraging cutting-edge AI voice technology without requiring complex native development.
🎯 Project Overview
Alpha Agent transforms the ElevenLabs conversational AI widget into a mobile-first voice assistant experience. Unlike traditional chatbots, Alpha Agent provides:

Full voice conversations: Speak naturally and receive AI voice responses
Professional voice quality: 5,000+ voices across 31 languages via ElevenLabs
Instant setup: Works immediately with Expo Go - no Android SDK required
Mobile-optimized UI: Custom WebView integration with full-screen widget positioning

🚀 Quick Start
bash# Clone and setup
git clone <your-repo-url>
cd alpha-agent
npm install

# Start development (works with Expo Go)
npx expo start

# Scan QR code with Expo Go app on your phone
Requirements:

Node.js 20+ (Node 18 reached EOL April 30, 2025)
Expo Go app on your mobile device
ElevenLabs account and agent ID

🏗️ Technical Architecture
Core Technologies

Expo SDK 53 (April 2025 release)
React Native 0.79 with New Architecture
React 19 (latest stable)
ElevenLabs Conversational AI Widget

Key Design Decisions
WebView Integration Approach
We use react-native-webview instead of DOM Components to maintain Expo Go compatibility:
typescript// Full-screen widget positioning solution
const elevenLabsHTML = `
  <elevenlabs-convai 
    agent-id="your-agent-id"
    style="position: fixed !important; top: 0 !important; 
           width: 100vw !important; height: 100vh !important;"
  ></elevenlabs-convai>
`;
Why WebView over DOM Components:

✅ Works with Expo Go (no development builds needed)
✅ No Android SDK/Java requirements
✅ Instant testing and iteration
✅ Simple deployment workflow

Widget Placement Solution
The ElevenLabs widget defaults to bottom-right positioning on websites. Our solution:

CSS Override Strategy: Force full-screen positioning with !important declarations
Mobile-First Layout: Viewport optimizations for touch interfaces
Custom Container: Eliminates web-style floating behavior

📱 App Flow
User Opens App → Taps "Start Voice Assistant" → WebView Loads → Widget Appears Full-Screen
     ↓
User Speaks → ElevenLabs Processes → AI Responds with Voice → Conversation Continues
🎤 Voice Capabilities
Input Processing

Natural speech recognition in 31 languages
Real-time audio processing
Noise handling and voice activity detection

Output Generation

Professional AI voice synthesis
Emotional expression and natural intonation
Configurable voice personalities and languages

Conversation Features

Multi-turn dialogue with context retention
Interrupt handling for natural conversation flow
Custom personality and knowledge base integration

📦 Package Dependencies
json{
  "expo": "~53.0.0",
  "react": "19.0.0",
  "react-native": "0.79.0", 
  "react-native-webview": "^13.10.5",
  "expo-speech": "~12.0.0",
  "expo-audio": "~2.0.0"
}
Note: expo-av is deprecated in SDK 53. We use expo-audio for enhanced audio capabilities.
🔧 Configuration
app.json Setup
json{
  "expo": {
    "name": "Alpha Agent",
    "slug": "alpha-agent",
    "version": "1.0.0",
    "platforms": ["ios", "android"],
    "newArchEnabled": true,
    "permissions": ["RECORD_AUDIO"]
  }
}
ElevenLabs Integration

Create account at ElevenLabs
Set up conversational AI agent
Copy agent ID to replace agent_4601k19n9bvhf1m9c4bmsnj5e39t

🎨 UI/UX Design
Start Screen

Minimalist dark theme
Single prominent "Start Voice Assistant" button
Clear visual feedback and loading states

Voice Interface

Full-screen conversational widget
Subtle header with status indicators
Clean, distraction-free design optimized for voice interaction

Visual Feedback

Speaking indicators during voice input
AI processing states
Connection status and error handling

🧪 Development Workflow
Context Engineering Approach
This project uses context engineering principles for AI-assisted development:
bash# Generate comprehensive implementation plans
/generate-prp INITIAL.md

# Execute features with full context
/execute-prp PRPs/voice-interface.md
Testing Strategy

Expo Go Testing: Rapid iteration on real devices
Voice Quality Testing: Multi-language and accent validation
Performance Testing: Memory usage and battery optimization
Error Handling: Network failure and permission edge cases

🚀 Deployment Options
Development (Expo Go)
bashnpx expo start
# Scan QR code with Expo Go
Production (EAS Build)
bash# Install EAS CLI
npm install -g @expo/eas-cli

# Configure and build
eas build:configure
eas build --platform android
🔮 Future Enhancements
Phase 1: Core Voice Experience ✅

 WebView ElevenLabs integration
 Full-screen widget positioning
 Two-way voice conversation

Phase 2: Advanced Features

 Wake word detection ("Hey Alpha")
 Background listening capabilities
 Custom voice training
 Conversation history and context

Phase 3: Native Optimization

 Migrate to development builds for performance
 Implement native speech recognition
 Add biometric authentication
 Offline capabilities

📊 Performance Considerations
Memory Usage

WebView overhead: ~50-100MB additional memory
Widget bundle: 601KB initial load
Audio streaming: Minimal impact with efficient buffering

Battery Optimization

Manual activation prevents always-listening battery drain
Efficient audio processing with expo-audio
Smart connection management

Network Requirements

Initial widget load: ~1MB
Voice streaming: ~50KB/second during conversation
Offline graceful degradation planned

🛠️ Troubleshooting
Common Issues
Widget not loading:
typescript// Check WebView permissions
<WebView
  javaScriptEnabled={true}
  domStorageEnabled={true}
  mediaPlaybackRequiresUserAction={false}
/>
Audio not playing:
typescript// Ensure audio mode setup
await Audio.setAudioModeAsync({
  playsInSilentModeIOS: true,
  allowsRecordingIOS: true
});
Widget positioning issues:

Verify CSS !important declarations
Check viewport meta tag
Test on multiple device sizes

📝 Contributing

Fork the repository
Create feature branch (git checkout -b feature/amazing-feature)
Follow context engineering patterns in /examples
Test with Expo Go on real devices
Submit pull request with comprehensive context

📄 License
MIT License - see LICENSE file for details
🙏 Acknowledgments

ElevenLabs for conversational AI technology
Expo for cross-platform development framework
Context Engineering methodology
React Native community for WebView implementations
