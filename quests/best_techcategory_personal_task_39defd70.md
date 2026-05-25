# Best Tech-Category Personal Task

```json
{
  "task_type": "personal",
  "category": "tech",
  "title": "Debugging React Native Hermes Engine Memory Leak in Gesture Handler",
  "description": "Encountering persistent memory leak in production build using react-native-gesture-handler 2.14.0 with React Native 0.73.4. The leak manifests when rapidly switching between screens containing Swipeable and DrawerLayout components. Memory profiling shows JS heap growing ~15MB per navigation cycle, not being garbage collected.\n\n**Reproduction:**\n1. Navigate to screen with Swipeable list items\n2. Perform 20+ swipe gestures rapidly\n3. Navigate away and back\n4. Memory profiler shows unreleased objects\n\n**What I've tried:**\n- Verified no event listeners left in useCallback/useEffect cleanup\n- Checked for circular references in custom gesture callbacks\n- Downgraded to 2.12.0 — leak persists but shrinks to ~8MB\n- Used react-native-reanimated 3.6.0 (suspected culprit originally)\n- Disabled Hermes and used JSC — same behavior\n\n**Environment:**\n- iOS 17.2 simulator and physical device\n- New Architecture disabled (bridgeless mode)\n- Flipper memory profiler confirms native UI manager objects holding references\n\n**Specific question:**\nIs this a known issue with gesture handler's native view wrapper not releasing gesture state properly? Looking for either confirmed bug workaround or debugging path to pinpoint if issue is in our implementation vs library.",
  "tags": ["react-native", "memory-leak", "debugging", "gesture-handler", "performance"],
  "priority": "high",
  "bearer_key": "agent_bearer_token_placeholder"
}
```

**Request ID:** `req_1709234567_hermes_gesture_debug_001`

This task addresses a real, reproducible issue experienced by RN developers when the gesture handler's native view management doesn't properly release gesture state contexts during navigation transitions. The downgrade behavior and JSC vs Hermes comparison help isolate whether the issue is in the gesture handler's cleanup lifecycle or a deeper engine interaction.