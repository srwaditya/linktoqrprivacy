# LINKTOQR - QR Code Generator Chrome Extension

## Single Purpose
An extension must have a single purpose that is narrow and easy to understand

**LINKTOQR's Purpose:** Convert any URL or text into a scannable QR code with a single click, enabling seamless sharing and quick access to web content.

---

## Overview
LINKTOQR is a powerful Chrome extension that enables users to generate, customize, and share QR codes instantly. The extension offers both free and premium features for QR code generation and management.

**Version:** 1.0.0  
**License:** MIT  
**Author:** srwaditya

---

## Table of Contents
1. [Project Structure](#project-structure)
2. [Features](#features)
3. [Permissions & Justifications](#permissions--justifications)
4. [File Documentation](#file-documentation)
5. [Installation](#installation)
6. [Development](#development)

---

## Project Structure

```
linktoqr-extension/
├── manifest.json                 # Extension configuration
├── package.json                  # Project metadata
├── src/
│   ├── css/
│   │   └── styles.css           # UI styling
│   ├── html/
│   │   ├── popup.html           # Main popup interface
│   │   └── shared-card.html     # Shared card component
│   ├── images/                  # Extension icons
│   │   ├── icon-16.png
│   │   ├── icon-48.png
│   │   └── icon-128.png
│   └── js/
│       ├── background.js        # Service worker
│       ├── popup.js             # Popup logic
│       ├── premium.js           # Premium features
│       ├── storage.js           # Data persistence
│       ├── ui.js                # UI utilities
│       └── lib/
│           └── qrcode.min.js    # QR code generation library
```

---

## Features

### Core Functionality
- **QR Code Generation:** Instantly generate QR codes from URLs and text
- **Customization:** Customize QR code appearance and format
- **Easy Sharing:** Share generated QR codes with others
- **Free & Premium Tiers:** Flexible feature set for different user needs

### Supported Capabilities
- Generate QR codes from the current active tab
- Store QR codes for later access
- Download QR codes
- Copy QR codes to clipboard
- Premium features for enhanced functionality

---

## Permissions & Justifications

### activeTab
**Purpose:** Access the currently active tab to generate QR codes  
**Justification:** Required to read the URL of the current webpage and generate a QR code representing that URL. This permission only applies to the tab the user explicitly clicks on.

### scripting
**Purpose:** Execute scripts in web pages  
**Justification:** Allows the extension to inject QR code generation functionality into web pages and interact with page content when needed for enhanced QR code features.

### storage
**Purpose:** Store user data persistently  
**Justification:** Enables the extension to save user preferences, QR code history, premium account status, and other user-specific settings across browser sessions.

### clipboardWrite
**Purpose:** Copy generated QR codes to clipboard  
**Justification:** Allows users to quickly copy generated QR codes to their clipboard for easy pasting into other applications or documents.

### download
**Purpose:** Download generated QR codes  
**Justification:** Enables users to download generated QR codes as image files to their computer for sharing, printing, or archival purposes.

### host_permissions (`<all_urls>`)
**Purpose:** Access all websites  
**Justification:** Allows the extension to generate QR codes from any URL the user visits. This broad permission enables the extension to function seamlessly across all web pages without requiring site-specific permissions, providing a better user experience while respecting user privacy through the activeTab permission requirement.

---

## File Documentation

### Manifest Configuration (`manifest.json`)
- **Manifest Version:** 3 (Latest Chrome extension format)
- **Host Permissions:** Access to all URLs (`<all_urls>`)
- **Action:** Defines popup interface and extension icons
- **Background Service Worker:** Handles long-running tasks and events
- **Web Accessible Resources:** QR code library available to all pages

### Package Configuration (`package.json`)
- **Main Entry Point:** `src/js/popup.js`
- **Dependencies:** No external npm dependencies (self-contained)
- **Scripts:** Development and build commands included

### JavaScript Files

#### `background.js`
Service worker that runs in the background to:
- Handle extension lifecycle events
- Manage message passing between popup and content scripts
- Process QR code generation requests
- Store and retrieve data

#### `popup.js`
Main popup interface controller that:
- Initializes the popup UI
- Handles user interactions
- Manages QR code generation form
- Communicates with background service worker

#### `premium.js`
Premium feature management including:
- Premium account status checking
- Premium-only feature validation
- Feature unlock logic
- Premium content rendering

#### `storage.js`
Data persistence layer for:
- Storing QR code history
- Saving user preferences
- Managing account information
- Caching generated QR codes

#### `ui.js`
UI utilities for:
- DOM manipulation
- Event binding
- UI state management
- Component rendering

#### `qrcode.min.js` (Library)
Minified QR code generation library that:
- Generates QR codes from text/URLs
- Supports various QR code formats
- Handles encoding and error correction

### HTML Files

#### `popup.html`
Main extension popup interface containing:
- Input field for URL/text entry
- QR code display area
- Action buttons (download, copy, share)
- Settings/preferences section
- Premium feature indicators

#### `shared-card.html`
Shared card component for:
- Displaying QR codes in a card format
- Sharing functionality
- Preview rendering

### Styles (`styles.css`)
CSS styling for:
- Popup interface layout
- Button and form styling
- Responsive design
- Premium feature styling
- Dark/light theme support

---

## Installation

### For Users
1. Download the extension from Chrome Web Store (when published)
2. Click "Add to Chrome"
3. Confirm the permission request
4. Extension icon appears in the toolbar

### For Developers
1. Clone the repository
2. Open Chrome and navigate to `chrome://extensions/`
3. Enable "Developer mode" (top right)
4. Click "Load unpacked"
5. Select the `linktoqr-extension` folder
6. Extension is now loaded for development

---

## Development

### Running in Development Mode
```bash
npm run dev
```
Then load the unpacked extension in Chrome DevTools.

### Building
```bash
npm run build
```

### Testing
```bash
npm test
```

### Directory Structure Notes
- All code is vanilla JavaScript (no build step required)
- QR code generation uses the `qrcode.min.js` library
- All dependencies are self-contained within the `src/` directory

---

## Extension Architecture

### Message Flow
1. **Popup** → User triggers QR code generation
2. **Popup.js** → Sends message to background service worker
3. **Background.js** → Processes request, generates QR code
4. **Storage.js** → Persists data if needed
5. **Popup.js** → Receives response and displays QR code

### Data Storage
- User preferences stored in Chrome's `storage.sync` API
- QR code history maintained in browser storage
- Premium account status cached locally

---

## Troubleshooting

- **Extension not working:** Ensure all permissions are granted
- **QR codes not generating:** Check that qrcode.min.js library is properly loaded
- **Data not persisting:** Verify storage permissions are enabled

---

## Support & Contributing
For issues, feature requests, or contributions, please contact the development team or create an issue in the repository.

---

**Last Updated:** February 2026
