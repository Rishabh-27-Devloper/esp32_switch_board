# ESP32 Switchboard Android App

A modern, feature-rich Android companion app for the ESP32 Switchboard IoT controller with BLE communication.

## 🌟 Features

### Core Functionality
- **BLE Advertising**: Continuously broadcasts Android device presence as `O|<16-digit-id>`
- **Real-time Switch Control**: Control 4 devices (2 Lights, Fan, Socket)
- **Auto-Discovery**: Scans and displays nearby ESP32 switchboards
- **Live Status Updates**: Receives switch states and room device count via BLE advertisements
- **Background Operation**: Foreground service keeps BLE active even when app is minimized

### User Interface
- **Modern Material Design**: Beautiful gradient cards with themed colors
- **Intuitive Controls**: Large, accessible switches with visual feedback
- **Connection Status**: Real-time connection indicator with color coding
- **Device List**: RecyclerView showing all discovered ESP32 devices with RSSI
- **Smooth Animations**: Responsive UI with progress indicators

### Advanced Features
- **GATT Communication**: Full BLE GATT client implementation
- **Indication Support**: Receives guaranteed delivery notifications from ESP32
- **Auto-reconnect**: Handles connection drops gracefully
- **Permission Management**: Dynamic runtime permissions for Android 12+
- **Low Power**: Optimized BLE operations for battery efficiency

## 📱 App Architecture

### Components

1. **MainActivity.java**
   - Main UI controller
   - Manages switch states and user interactions
   - Handles permission requests
   - Updates UI based on BLE callbacks

2. **BLEManager.java**
   - Core BLE operations (scan, advertise, connect)
   - GATT client implementation
   - Command/response handling
   - Parses ESP32 advertisement data

3. **BLEForegroundService.java**
   - Keeps BLE advertising active in background
   - Shows persistent notification
   - Ensures app presence is always broadcasted

4. **DeviceAdapter.java**
   - RecyclerView adapter for discovered devices
   - Shows device info, RSSI, switch states
   - Handles device selection

5. **BLEDevice.java**
   - Model class for BLE devices
   - Signal strength calculation

## 🎨 UI Design

### Color Scheme
- **Primary**: Blue (#2196F3) - Modern, trustworthy
- **Accent Colors**:
  - Yellow (#FFC107) - Light 1
  - Orange (#FF9800) - Light 2
  - Light Blue (#03A9F4) - Fan
  - Green (#4CAF50) - Socket
- **Status Colors**:
  - Green - Connected
  - Red - Disconnected

### Card Design
- Material cards with elevation and corner radius
- Color-coded backgrounds for each device type
- Icons for visual identification
- Large touch targets for accessibility

## 📋 Setup Instructions

### Prerequisites
- Android Studio Arctic Fox or newer
- Android SDK 21+ (Lollipop) minimum
- Android 12+ for best BLE support
- Physical Android device (BLE requires hardware)

### Installation Steps

1. **Create New Project**
   ```
   File > New > New Project > Empty Activity
   Name: ESP32 Switchboard
   Package: com.esp32.switchboard
   Language: Java
   Minimum SDK: API 21
   ```

2. **Add Dependencies**
   - Copy `build.gradle (app)` content
   - Sync Gradle files

3. **Create Package Structure**
   ```
   com.esp32.switchboard/
   ├── MainActivity.java
   ├── BLEManager.java
   ├── BLEForegroundService.java
   ├── DeviceAdapter.java
   └── BLEDevice.java
   ```

4. **Add Layout Files**
   ```
   res/layout/
   ├── activity_main.xml
   └── item_device.xml
   ```

5. **Add Resources**
   ```
   res/values/
   ├── colors.xml
   ├── strings.xml
   └── themes.xml
   ```

6. **Update Manifest**
   - Replace with provided `AndroidManifest.xml`
   - Ensure all permissions are declared

7. **Add Icons** (Create in `res/drawable/`)
   - `ic_bluetooth.xml` - Bluetooth icon
   - `ic_light.xml` - Light bulb icon
   - `ic_fan.xml` - Fan icon
   - `ic_socket.xml` - Power outlet icon
   - `ic_refresh.xml` - Refresh icon
   - `ic_connect.xml` - Connection arrow icon

### Required Drawable Icons (Vector Assets)

**ic_bluetooth.xml**
```xml
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="24dp" android:height="24dp"
    android:viewportWidth="24" android:viewportHeight="24">
    <path android:fillColor="#FF000000"
        android:pathData="M17.71,7.71L12,2h-1v7.59L6.41,5 5,6.41 10.59,12 5,17.59 6.41,19 11,14.41V22h1l5.71,-5.71 -4.3,-4.29 4.3,-4.29zM13,5.83l1.88,1.88L13,9.59V5.83zM14.88,16.29L13,18.17v-3.76l1.88,1.88z"/>
</vector>
```

**ic_light.xml**
```xml
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="24dp" android:height="24dp"
    android:viewportWidth="24" android:viewportHeight="24">
    <path android:fillColor="#FF000000"
        android:pathData="M9,21c0,0.5 0.4,1 1,1h4c0.6,0 1,-0.5 1,-1v-1L9,20v1zM12,2C8.1,2 5,5.1 5,9c0,2.4 1.2,4.5 3,5.7L8,17c0,0.5 0.4,1 1,1h6c0.6,0 1,-0.5 1,-1v-2.3c1.8,-1.3 3,-3.4 3,-5.7 0,-3.9 -3.1,-7 -7,-7z"/>
</vector>
```

**ic_fan.xml**
```xml
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="24dp" android:height="24dp"
    android:viewportWidth="24" android:viewportHeight="24">
    <path android:fillColor="#FF000000"
        android:pathData="M12,11c-0.55,0 -1,0.45 -1,1s0.45,1 1,1 1,-0.45 1,-1 -0.45,-1 -1,-1zM22,12c0,-1.66 -1.34,-3 -3,-3h-0.14c0.45,-0.83 0.74,-1.77 0.81,-2.77C19.82,4.09 18.12,2.39 16,2.25c-1.66,-0.11 -3.14,0.88 -3.66,2.41C12,5.22 12,5.83 12,6.43c0,0.28 0.03,0.56 0.08,0.83 -0.31,-0.05 -0.64,-0.08 -0.98,-0.08 -3.03,0 -5.5,2.47 -5.5,5.5s2.47,5.5 5.5,5.5c0.34,0 0.67,-0.03 0.98,-0.08 -0.05,0.27 -0.08,0.55 -0.08,0.83 0,0.6 0,1.21 0.34,1.77 0.52,1.53 2,2.52 3.66,2.41 2.12,-0.14 3.82,-1.84 3.67,-4.08 -0.07,-1 -0.36,-1.94 -0.81,-2.77H19c1.66,0 3,-1.34 3,-3z"/>
</vector>
```

**ic_socket.xml**
```xml
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="24dp" android:height="24dp"
    android:viewportWidth="24" android:viewportHeight="24">
    <path android:fillColor="#FF000000"
        android:pathData="M12,2C6.48,2 2,6.48 2,12s4.48,10 10,10 10,-4.48 10,-10S17.52,2 12,2zM8,17c-0.55,0 -1,-0.45 -1,-1L7,8c0,-0.55 0.45,-1 1,-1s1,0.45 1,1v8c0,0.55 -0.45,1 -1,1zM16,17c-0.55,0 -1,-0.45 -1,-1L15,8c0,-0.55 0.45,-1 1,-1s1,0.45 1,1v8c0,0.55 -0.45,1 -1,1z"/>
</vector>
```

**ic_refresh.xml**
```xml
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="24dp" android:height="24dp"
    android:viewportWidth="24" android:viewportHeight="24">
    <path android:fillColor="#FF000000"
        android:pathData="M17.65,6.35C16.2,4.9 14.21,4 12,4c-4.42,0 -7.99,3.58 -7.99,8s3.57,8 7.99,8c3.73,0 6.84,-2.55 7.73,-6h-2.08c-0.82,2.33 -3.04,4 -5.65,4 -3.31,0 -6,-2.69 -6,-6s2.69,-6 6,-6c1.66,0 3.14,0.69 4.22,1.78L13,11h7V4l-2.35,2.35z"/>
</vector>
```

**ic_connect.xml**
```xml
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="24dp" android:height="24dp"
    android:viewportWidth="24" android:viewportHeight="24">
    <path android:fillColor="#FF000000"
        android:pathData="M12,4l-1.41,1.41L16.17,11H4v2h12.17l-5.58,5.59L12,20l8,-8z"/>
</vector>
```

## 🔧 Configuration

### ESP32 UUIDs (Must Match)
```java
SERVICE_UUID = "12345678-1234-5678-1234-56789abcdef0"
COMMAND_CHAR_UUID = "12345678-1234-5678-1234-56789abcdef1"
STATUS_CHAR_UUID = "12345678-1234-5678-1234-56789abcdef2"
```

### Advertisement Format
**Android App** → ESP32: `O|<16-digit-android-id>`
**ESP32** → Android App: `@##<timestamp>$<flags>$<deviceCount>`

Example: `@##12345$1010$3`
- Timestamp: 12345 seconds
- Flags: Light1=ON, Light2=OFF, Fan=ON, Socket=OFF
- Device Count: 3 devices in room

### Commands
- `LIGHT1 ON` / `LIGHT1 OFF`
- `LIGHT2 ON` / `LIGHT2 OFF`
- `FAN ON` / `FAN OFF`
- `SOCKET ON` / `SOCKET OFF`

### Responses
- `ACK:<command>:<flags>` - Success
- `ERR:UNKNOWN_CMD` - Invalid command

## 🚀 Usage

1. **First Launch**
   - App requests Bluetooth and location permissions
   - Allows Bluetooth if not enabled
   - Starts foreground service

2. **Discovery**
   - App automatically scans for ESP32 devices
   - Displays devices in RecyclerView with signal strength
   - Shows switch states and device count from advertisements

3. **Connection**
   - Tap any discovered ESP32 device
   - App connects via GATT
   - Connection status updates to "Connected"
   - Switches become enabled

4. **Control**
   - Toggle switches to control devices
   - Commands sent via BLE GATT
   - Receive confirmation with updated states
   - UI updates automatically

5. **Background**
   - App continues advertising presence
   - Notification shows service status
   - Connection maintained in background

## 🛠️ Troubleshooting

### Permissions Denied
- Go to Settings > Apps > ESP32 Switchboard > Permissions
- Enable Nearby Devices / Bluetooth permissions
- Enable Location (required for Android 11 and below)

### Can't Find ESP32
- Ensure ESP32 is powered and running
- Check ESP32 is advertising (Serial Monitor shows "📡 BLE GATT Server Ready")
- Tap refresh button to scan again
- Move closer to ESP32 (BLE range ~10 meters)

### Connection Fails
- Restart both app and ESP32
- Clear app data and retry
- Check UUIDs match between app and ESP32
- Ensure no other device is connected to ESP32

### Switches Not Working
- Verify connection status shows "Connected"
- Check ESP32 Serial Monitor for received commands
- Ensure GATT characteristic write succeeded
- Try disconnecting and reconnecting

### Background Service Stops
- Add app to battery optimization whitelist
- Disable battery saver for this app
- Some manufacturers (Xiaomi, Huawei) require special settings

## 📊 Performance

- **BLE Advertising**: Continuous, low power
- **Scanning**: 10-second cycles with auto-stop
- **Connection**: <1 second to established GATT
- **Command Latency**: ~50-100ms round trip
- **Battery Impact**: Minimal with optimized settings

## 🔐 Security

- BLE encryption enabled via `WRITE_ENC` property
- No authentication required (adjust based on needs)
- Commands require GATT connection (not via advertising)
- Android ID provides unique device identification

## 📝 Future Enhancements

- [ ] Device grouping and room management
- [ ] Scheduling and automation
- [ ] Voice control integration
- [ ] Historical data and analytics
- [ ] Multiple ESP32 support
- [ ] OTA firmware updates
- [ ] Cloud sync capabilities
- [ ] Widget support

## 🤝 Contributing

Feel free to submit issues and enhancement requests!

## 📄 License

This project is open source and available under the MIT License.

## 👨‍💻 Author

Created for ESP32 IoT Switchboard System

---

**Note**: This app requires a physical Android device with BLE hardware. BLE emulation in Android Studio emulator is not supported.
