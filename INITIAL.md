# INITIAL.md

## FEATURE:
Build Alpha Agent - a complete Siri-like voice assistant mobile app using Expo SDK 53 and ElevenLabs Conversational AI widget. The app must provide natural two-way voice conversations with professional AI voice responses, optimized for mobile devices, and compatible with Expo Go for rapid development and testing.

### Core Functionality Requirements:
1. **Voice Input & Output**: Users speak naturally to the AI and receive spoken responses using ElevenLabs' premium voice synthesis (5,000+ voices, 31 languages)
2. **Mobile-First Interface**: Clean, intuitive UI with manual activation (tap button to start voice session)
3. **Full-Screen Voice Experience**: ElevenLabs widget fills entire screen, eliminating web-style bottom positioning issues
4. **Real-Time Conversation**: Continuous voice dialogue with context retention and natural conversation flow
5. **Expo Go Compatibility**: Must work immediately in Expo Go without requiring development builds or Android SDK
6. **Cross-Platform**: Identical experience on iOS and Android devices

### Technical Implementation Requirements:
- **Expo SDK 53** (latest stable, released April 30, 2025)
- **React Native 0.79** with New Architecture enabled by default
- **React 19** integration
- **react-native-webview** for ElevenLabs widget embedding (NOT DOM Components to maintain Expo Go compatibility)
- **expo-audio** for audio management (expo-av is deprecated in SDK 53)
- **expo-speech** for fallback text-to-speech capabilities
- **TypeScript** with strict mode for type safety

### User Experience Flow:
```
App Launch → Welcome Screen → Tap "Start Voice Assistant" → Widget Loads Full-Screen → 
User Speaks → AI Processes → AI Responds with Voice → Continuous Conversation → 
Tap "End Session" → Return to Welcome Screen
```

### Widget Integration Challenges to Solve:
1. **Positioning Override**: ElevenLabs widget defaults to bottom-right corner on websites - must be forced to full-screen
2. **Mobile Touch Optimization**: Ensure proper touch handling and gesture recognition within WebView
3. **Audio Configuration**: Proper iOS/Android audio permissions and WebView audio settings
4. **Loading States**: Smooth widget initialization with appropriate loading feedback
5. **Error Handling**: Graceful fallbacks when widget fails to load or network issues occur

## EXAMPLES:
Reference these example patterns that should be implemented in the project:

### Audio Integration Pattern (`examples/audio-setup.tsx`):
```typescript
// Proper expo-audio configuration for SDK 53
import { Audio } from 'expo-audio';

const setupAudio = async () => {
  await Audio.setAudioModeAsync({
    allowsRecordingIOS: true,
    staysActiveInBackground: false,
    playsInSilentModeIOS: true,
    shouldDuckAndroid: true,
    playThroughEarpieceAndroid: false,
  });
};
```

### WebView Widget Positioning (`examples/webview-fullscreen.tsx`):
```typescript
// CSS override strategy for forcing full-screen widget
const elevenLabsHTML = `
  <style>
    elevenlabs-convai {
      position: fixed !important;
      top: 0 !important;
      left: 0 !important;
      width: 100vw !important;
      height: 100vh !important;
      border: none !important;
      z-index: 9999 !important;
    }
  </style>
`;
```

### Mobile-Optimized WebView Configuration (`examples/webview-config.tsx`):
```typescript
<WebView
  javaScriptEnabled={true}
  domStorageEnabled={true}
  mediaPlaybackRequiresUserAction={false}
  allowsInlineMediaPlayback={true}
  scalesPageToFit={false}
  showsVerticalScrollIndicator={false}
  scrollEnabled={false}
  bounces={false}
/>
```

### Component Architecture Pattern (`examples/voice-component-structure.tsx`):
- Main App component with state management
- VoiceAssistant screen component
- Custom hooks for audio permissions and WebView management
- Error boundary components for production stability
- Loading state components with proper UX feedback

### Permission Handling Pattern (`examples/permissions.tsx`):
Proper iOS/Android audio permission requests with fallback handling and user-friendly messaging.

## DOCUMENTATION:

### Expo SDK 53 Documentation:
- **Expo SDK 53 Release Notes**: https://expo.dev/changelog/2024-11-12-sdk-52 (for reference, SDK 53 notes)
- **New Architecture Documentation**: https://docs.expo.dev/ (New Architecture enabled by default)
- **expo-audio API Reference**: https://docs.expo.dev/versions/latest/sdk/audio/ (replaces expo-av)
- **expo-speech API Reference**: https://docs.expo.dev/versions/latest/sdk/speech/
- **react-native-webview Documentation**: https://github.com/react-native-webview/react-native-webview

### ElevenLabs Integration:
- **Conversational AI Widget Documentation**: https://elevenlabs.io/docs/conversational-ai/widget
- **Widget Embed Script**: `https://unpkg.com/@elevenlabs/convai-widget-embed`
- **Widget Configuration Options**: Agent ID setup, theme customization, event handling
- **Voice Models and Languages**: 5,000+ voices across 31 languages documentation

### React Native 0.79 Specific:
- **React Native 0.79 Upgrade Guide**: Breaking changes and new features
- **React 19 Integration Notes**: Component updates and hook changes
- **New Architecture Migration**: Turbo Modules and Fabric renderer

### Mobile Development Best Practices:
- **React Native Performance**: Memory management, rendering optimization
- **Audio Handling**: iOS AVAudioSession, Android AudioManager integration
- **WebView Security**: Origin whitelisting, content security policies

## OTHER CONSIDERATIONS:

### Critical Implementation Details:

1. **Package Version Compatibility**:
   - Verify all packages work with Expo SDK 53 and New Architecture
   - expo-av is DEPRECATED - must use expo-audio instead
   - Node.js 20+ required (Node 18 reached EOL April 30, 2025)
   - Xcode 16.2+ required for iOS builds

2. **WebView vs DOM Components Decision**:
   - Use WebView approach instead of DOM Components to maintain Expo Go compatibility
   - DOM Components require development builds (not suitable for rapid prototyping)
   - WebView allows immediate testing with Expo Go app

3. **Widget Positioning Critical Issue**:
   - ElevenLabs widget has hardcoded bottom positioning for web
   - Must use CSS `!important` overrides to force full-screen
   - Test on multiple device sizes (iPhone SE, iPhone Pro Max, various Android)
   - Ensure touch events work properly in repositioned widget

4. **Audio Configuration Gotchas**:
   - iOS requires explicit silent mode override for voice playback
   - Android needs proper audio focus management
   - WebView audio requires `mediaPlaybackRequiresUserAction={false}`
   - Test with device in silent mode, headphones, and Bluetooth audio

5. **Performance Considerations**:
   - WebView adds ~50-100MB memory overhead
   - Widget bundle is 601KB initial load
   - Implement proper loading states and error boundaries
   - Monitor battery usage during extended voice sessions

6. **Permission Handling Edge Cases**:
   - Handle microphone permission denial gracefully
   - Provide clear instructions for enabling permissions
   - Test permission re-requests after initial denial
   - Different permission flows on iOS vs Android

7. **Network Failure Scenarios**:
   - Widget fails to load due to poor connectivity
   - Voice streaming interruptions during conversation
   - Fallback to expo-speech for basic text-to-speech
   - Offline mode considerations and user messaging

8. **ElevenLabs Agent Configuration**:
   - Agent ID must be configurable (not hardcoded)
   - Test with different voice personalities and languages
   - Handle agent rate limits and quota management
   - Conversation context and memory settings

9. **Development Workflow Considerations**:
   - Use `npx expo start --tunnel` for HTTPS requirement during development
   - Test on physical devices, not just simulators
   - ElevenLabs widget requires secure context (HTTPS)
   - Expo Go app must be latest version supporting SDK 53

10. **Production Deployment Gotchas**:
    - App store approval considerations for voice recording
    - Privacy policy requirements for voice data processing
    - ElevenLabs terms of service compliance
    - Rate limiting and cost management for voice API usage

### Common AI Assistant Mistakes to Avoid:
- Don't use deprecated packages (expo-av, old WebView configs)
- Don't assume DOM Components work with Expo Go
- Don't ignore CSS positioning issues with the widget
- Don't forget audio permission handling on both platforms
- Don't hardcode ElevenLabs agent IDs or API keys
- Don't neglect WebView security configurations
- Don't assume widget will work without HTTPS in development
- Don't forget to test voice functionality on real devices
- Don't ignore memory management for long voice sessions
- Don't overlook fallback scenarios when widget fails to load

### Success Criteria Validation:
1. App loads successfully in Expo Go on both iOS and Android
2. Voice assistant starts when button is tapped
3. User can speak and receive AI voice responses
4. Widget fills entire screen without positioning issues
5. Audio works properly with device in silent mode
6. Proper error handling for network failures and permission denials
7. Smooth conversation flow with context retention
8. Professional voice quality matches ElevenLabs standards
9. App remains responsive during voice interactions
10. Clean exit from voice session returns to welcome screen
