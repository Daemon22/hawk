# Hawk - Device Detection Monitor

## Introduction
Hawk is a comprehensive, modular JavaScript library designed for robust and accurate device and environment detection across various platforms. Developed by Uviwe Menyiwe (Azura) from the Hael Foundation, Hawk provides a standardized device profile output, making it an essential tool for developers needing to adapt their applications to different user contexts.

## Features
- **Cross-Platform Compatibility**: Detects environments on mobile, desktop, terminal, and hybrid setups.
- **Multiple Detection Methods**: Leverages user agent strings, native APIs, and OS-specific modules for precise detection.
- **Standardized Output**: Provides a consistent and easy-to-parse device profile.
- **Modular and Extensible**: Designed with a modular architecture, allowing for easy integration of custom detectors.
- **Caching Mechanism**: Improves performance by caching detection results with a configurable TTL (Time-To-Live).
- **Debug Mode**: Offers a debug mode for detailed logging during development.

## Installation

### Browser
```html
<script src="path/to/hawk.js"></script>
<script>
  const monitor = new DeviceMonitor();
  monitor.detect().then(profile => {
    console.log(profile);
  });
</script>
```

### Node.js
```javascript
const DeviceMonitor = require("./path/to/hawk.js");

async function getDeviceProfile() {
  const monitor = new DeviceMonitor({ debugMode: true });
  const profile = await monitor.detect();
  console.log(profile);
}

getDeviceProfile();
```

## Usage

### Basic Usage
```javascript
const monitor = new DeviceMonitor();
monitor.detect().then(profile => {
  console.log("Device Profile:", profile);
});
```

### Configuration Options

| Option          | Type      | Default     | Description                                                               |
| :-------------- | :-------- | :---------- | :------------------------------------------------------------------------ |
| `enableCache`   | `boolean` | `true`      | Enables or disables caching of detection results.                         |
| `cacheTTL`      | `number`  | `300000` ms | Time-To-Live for cached results in milliseconds (5 minutes).              |
| `debugMode`     | `boolean` | `false`     | Enables console logging for debugging purposes.                           |
| `customDetectors` | `Array`   | `[]`        | An array of custom detector instances to extend Hawk's capabilities.      |

Example with options:
```javascript
const monitor = new DeviceMonitor({
  enableCache: true,
  cacheTTL: 600000, // 10 minutes
  debugMode: true,
  customDetectors: [/* your custom detectors here */]
});

monitor.detect().then(profile => {
  console.log("Debug Profile:", profile);
});
```

### Clearing the Cache
```javascript
monitor.clearCache();
console.log("Cache cleared.");
```

## API Reference

### `DeviceMonitor` Class

#### `constructor(options)`
Initializes the `DeviceMonitor` instance with the given options.

**Parameters:**
- `options` (Object, optional): Configuration options for the monitor.

#### `detect()`
Asynchronously detects and returns a comprehensive device profile.

**Returns:** `Promise<Object>` - A promise that resolves with the device profile object.

#### `clearCache()`
Clears the internally cached device profile, forcing a fresh detection on the next `detect()` call.

## Device Profile Structure

The `detect()` method returns an object with the following structure:

```javascript
{
  timestamp: "2024-01-15T10:30:00.000Z",
  os: {
    name: "Windows",                    // e.g., "Windows", "macOS", "Android", "iOS", "Linux"
    version: "10",                      // e.g., "10", "14.4", "13"
    family: null,                       // e.g., "Windows", "macOS", "Linux"
    platform: "win32",                  // e.g., "win32", "darwin", "android", "ios", "linux"
    kernel: null,                       // Node.js specific
    distribution: null                  // Linux specific
  },
  deviceType: {
    type: "desktop",                    // e.g., "desktop", "mobile", "tablet", "tv", "wearable", "terminal", "unknown"
    formFactor: null,                   // e.g., "phone", "tablet", "desktop"
    manufacturer: null,                 // e.g., "Apple", "Samsung"
    model: null,                        // e.g., "iPhone 15", "Galaxy S23"
    isMobile: false,
    isTablet: false,
    isDesktop: true,
    isTV: false,
    isWearable: false,
    isTerminal: false
  },
  screen: {
    width: 1920,                        // Screen width in pixels
    height: 1080,                       // Screen height in pixels
    pixelRatio: 1,                      // Device pixel ratio
    colorDepth: 24,                     // Color depth in bits
    orientation: "landscape-primary",   // e.g., "portrait-primary", "landscape-primary"
    touchSupport: false,                // True if touch events are supported
    maxTouchPoints: 0                   // Maximum number of simultaneous touch contacts
  },
  architecture: {
    cpu: "x64",                         // e.g., "x64", "arm64", "x86"
    bits: 64,                           // e.g., 64, 32
    endian: null,                       // e.g., "little", "big"
    cores: null                         // Number of CPU cores
  },
  environment: {
    runtime: "browser",                 // e.g., "browser", "node", "electron", "react-native", "shell"
    runtimeVersion: null,               // e.g., "18.12.1", "1.0.0"
    isBrowser: true,
    isNode: false,
    isElectron: false,
    isReactNative: false,
    isShell: false,
    isHybrid: false,                    // True if running in a hybrid environment
    container: null,                    // e.g., "docker", "kubernetes"
    virtualization: null                // e.g., "vm"
  },
  capabilities: {
    webgl: true,
    webgpu: false,
    serviceWorker: true,
    localStorage: true,
    sessionStorage: true,
    indexedDB: true,
    geolocation: true,
    camera: false,
    microphone: false,
    bluetooth: false,
    usb: false,
    nfc: false,
    vibration: false,
    battery: false,
    networkInformation: false,
    shareAPI: true,
    clipboard: true,
    notifications: true,
    pushNotifications: false,
    paymentRequest: true,
    credentials: true
  },
  userAgent: "Mozilla/5.0 (Windows NT 10.0; Win64; x64)...",
  metadata: {
    timezone: "America/New_York",       // e.g., "America/New_York"
    language: "en-US",                  // e.g., "en-US"
    languages: ["en-US", "en"],         // Array of supported languages
    cookiesEnabled: true,
    doNotTrack: "1",                    // e.g., "1", "0", "unspecified"
    onlineStatus: true,
    hardwareConcurrency: 8,             // Number of logical processor cores
    deviceMemory: 16,                   // Device memory in GB
    maxTouchPoints: 0                   // Maximum number of simultaneous touch contacts
  }
}
```

## Contributing
Contributions are welcome! Please feel free to submit issues or pull requests.

## License
This project is licensed under the MIT License.

## Author
Uviwe Menyiwe (Azura) from the Hael Foundation
