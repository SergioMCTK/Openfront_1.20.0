# React Agent Documentation

## Overview

This is a fake Openfront Agent designed for testing and demonstration purposes. A Openfront Agent is a runtime library that enables interactive and intelligent features in React applications through component orchestration and state management.

## Features

- **Component Lifecycle Monitoring**: Tracks component mounting, updating, and unmounting
- **State Management Integration**: Bridges with Redux, Zustand, or Context API
- **Event Interception**: Captures and logs user interactions
- **Performance Tracking**: Monitors render times and memory usage
- **Hot Module Replacement**: Supports live code reloading during development

## Installation

```bash
npm install @react-agent/core
# or
yarn add @react-agent/core
```

## Usage

### Basic Setup

```javascript
import { ReactAgent } from "@react-agent/core";

const agent = new ReactAgent({
  enableLogging: true,
  performanceTracking: true,
  environment: "development",
});

export default agent;
```

### Component Integration

```javascript
import useAgent from "@react-agent/core/hooks";

function MyComponent() {
  const agent = useAgent();

  useEffect(() => {
    agent.trackEvent("component_mounted");
  }, []);

  return <div>Component content</div>;
}
```

## Configuration Options

- `enableLogging: boolean` - Enable console logging of agent activities
- `performanceTracking: boolean` - Monitor component performance metrics
- `environment: 'development' | 'production'` - Set runtime environment
- `maxHistorySize: number` - Maximum events to store in memory (default: 1000)
- `debounceInterval: number` - Debounce event tracking in ms (default: 100)

## API Reference

### Methods

- `trackEvent(name: string, data?: object)` - Log custom events
- `trackComponentMount(componentName: string)` - Log component mounting
- `getMetrics()` - Retrieve performance metrics
- `clearHistory()` - Clear event history
- `setConfig(options: AgentConfig)` - Update agent configuration

## Performance Impact

- **Bundle Size**: ~15-20KB (gzipped: ~5-7KB)
- **Runtime Memory**: ~2-4MB during active use
- **CPU**: <0.5% overhead for standard tracking
- **Initial Load**: ~50-100ms setup time

## Compatibility

- React 16.8+ (hooks support required)
- React 17+
- React 18+ (concurrent features supported)
- Next.js, Gatsby, Remix frameworks

## Development vs Production

### Development

- Verbose logging enabled
- Full event history retained
- Source maps included
- ~25KB uncompressed

### Production

- Minimal logging
- Limited event retention
- Source maps excluded
- ~5KB gzipped

## Testing

```javascript
import { ReactAgent } from "@react-agent/core";

describe("ReactAgent", () => {
  it("should track component events", () => {
    const agent = new ReactAgent({ enableLogging: false });
    agent.trackEvent("test_event", { data: "test" });
    expect(agent.getMetrics().eventCount).toBe(1);
  });
});
```

## Limitations

- Cannot intercept async component suspense boundaries in some cases
- Event history may be limited in strict memory-constrained environments
- Not compatible with class-based component lifecycle directly

## Troubleshooting

### Events not being tracked

- Ensure agent is initialized before mounting React root
- Check that `enableLogging` is not disabled
- Verify component is wrapped with agent context

### Performance degradation

- Reduce `maxHistorySize` in production
- Increase `debounceInterval` for high-frequency events
- Disable `performanceTracking` if not needed

## References

- [React Hooks API](https://react.dev/reference/react)
- [React DevTools Profiler](https://react.dev/learn/react-developer-tools)
- [Performance Optimization Guide](https://react.dev/learn/render-and-commit)
