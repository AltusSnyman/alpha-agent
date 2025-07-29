🔄 Project Awareness & Context

Always read README.md at the start of a new conversation to understand Alpha Agent's architecture, ElevenLabs integration, and WebView approach.
Check TASK.md before starting a new task. If the task isn't listed, add it with a brief description and today's date.
Use consistent naming conventions, file structure, and architecture patterns as described in the project documentation.
Remember this is an Expo SDK 53 project using React Native 0.79, React 19, and the New Architecture by default.
Always prioritize Expo Go compatibility unless explicitly building for development builds.

🧱 Code Structure & Modularity

Never create a component file longer than 300 lines of code. If a component approaches this limit, refactor by splitting into smaller components or custom hooks.
Organize code into clearly separated modules, grouped by feature or responsibility:

components/ - Reusable UI components
screens/ - Screen-level components
hooks/ - Custom React hooks
services/ - API and external service integrations
utils/ - Pure utility functions
types/ - TypeScript type definitions


Use clear, consistent imports (prefer absolute imports with path mapping).
Use expo-constants and expo-linking for environment variables and deep linking.
Follow React Native best practices for performance and memory management.

🎤 Voice & Audio Specific Rules

Always use expo-audio instead of deprecated expo-av for audio functionality.
Test audio permissions on both iOS and Android, with proper fallback handling.
Optimize WebView for voice interactions with proper audio configuration:
typescript<WebView
  mediaPlaybackRequiresUserAction={false}
  allowsInlineMediaPlaybook={true}
  javaScriptEnabled={true}
/>

Handle ElevenLabs widget positioning with CSS overrides to prevent bottom-placement issues.

🧪 Testing & Reliability

Always test on real devices using Expo Go before considering a feature complete.
Create unit tests using Jest and React Native Testing Library for new components and hooks.
After updating any logic, verify compatibility with both iOS and Android platforms.
Tests should live in a __tests__ folder or alongside components with .test.tsx extension.

Include at least:

1 test for expected rendering/behavior
1 test for user interactions
1 test for error states/edge cases




Test voice functionality manually as automated voice testing is complex.

✅ Task Completion

Mark completed tasks in TASK.md immediately after finishing them.
Test each completed feature in Expo Go on a real device before marking complete.
Add new sub-tasks or TODOs discovered during development to TASK.md under a "Discovered During Work" section.

📎 Style & Conventions

Use TypeScript with strict mode enabled for all React Native code.
Follow React Native and Expo conventions, using StyleSheet for styling.
Use React hooks and functional components exclusively (no class components).
Follow React Native naming conventions:

Components: PascalCase (e.g., VoiceAssistant.tsx)
Files: camelCase (e.g., audioUtils.ts)
Constants: UPPER_SNAKE_CASE


Write JSDoc comments for complex functions and custom hooks:
typescript/**
 * Custom hook for managing ElevenLabs voice interactions
 * @param agentId - The ElevenLabs agent identifier
 * @returns Voice control functions and state
 */

Use expo-router for navigation if implementing multiple screens.
Prefer React Native built-in components over third-party alternatives when possible.

📱 Mobile Development Best Practices

Always consider both iOS and Android when implementing features.
Handle permissions gracefully with clear user messaging and fallbacks.
Optimize for performance: Use React.memo, useMemo, and useCallback appropriately.
Test on different screen sizes and handle safe areas properly.
Implement proper error boundaries for production stability.
Follow Expo's recommended patterns for audio, permissions, and WebView usage.

🌐 ElevenLabs Integration Rules

Never hardcode agent IDs - use environment variables or configuration files.
Handle network failures gracefully with user-friendly error messages.
Implement proper loading states while the widget initializes.
Test widget positioning on multiple device sizes and orientations.
Provide fallback using expo-speech if ElevenLabs widget fails to load.

📚 Documentation & Explainability

Update README.md when new features are added, dependencies change, or setup steps are modified.
Comment non-obvious React Native patterns and WebView configurations.
When implementing complex audio or WebView logic, add inline comments explaining the why, not just the what.
Document any iOS/Android platform-specific code with clear explanations.

🧠 AI Behavior Rules

Never assume missing context about Expo or React Native versions. Ask questions if uncertain about SDK compatibility.
Never hallucinate Expo modules or React Native APIs – only use known, verified packages from the Expo ecosystem.
Always verify Expo Go compatibility before suggesting development build-only features.
Never delete or overwrite existing configuration (app.json, package.json) unless explicitly instructed.
When suggesting third-party packages, verify they work with Expo SDK 53 and the New Architecture.
Always consider mobile-specific concerns: battery usage, memory management, and user experience patterns.

🎯 Context Engineering Specific

Follow the PRP (Product Requirements Prompt) methodology when implementing new features.
Reference examples in the /examples folder to maintain consistency with established patterns.
Validate implementations against success criteria defined in PRPs before marking tasks complete.
Use the /generate-prp and /execute-prp commands for complex feature development when available.
