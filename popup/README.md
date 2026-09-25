# Lycaxia Notification

A lightweight notification system for modern JavaScript & React projects featuring **Toast**, **Log**, **Info**, **Confirm**, **Prompt**, **Dynamic Island**, multi-language support, and sound effects.

---

## Installation

### Vanilla JavaScript (CDN)

Simply include the script tag at the bottom of your HTML `<body>`. Styles are automatically injected, and the global `lyn` object will be exposed.

```html
<script src="[https://lib.lycaxia.com/notification/script.js](https://lib.lycaxia.com/notification/script.js)"></script>

```
### npm
Install the package via npm for module bundlers or React apps:
```bash
npm install lycaxia-notification

```
Import it in your JavaScript/TypeScript files:
```javascript
import lyn from "lycaxia-notification";

```
## Quick Start
### Vanilla Setup
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Lycaxia Example</title>
</head>
<body>

  <button onclick="showNotification()">Show Notification</button>

  <script src="[https://lib.lycaxia.com/notification/script.js](https://lib.lycaxia.com/notification/script.js)"></script>
  <script>
    lyn.soundNotification("allow");

    function showNotification() {
      lyn.toast({
        Title: "Hello!",
        Mess: "Lycaxia loaded successfully.",
        Status: "success"
      });
    }
  </script>

</body>
</html>

```
### React Setup
```jsx
import lyn from "lycaxia-notification";

function App() {
  const showNotification = () => {
    lyn.toast({
      Title: "Success",
      Mess: "Hello from React!",
      Status: "success"
    });
  };

  return (
    <button onClick={showNotification}>
      Show Notification
    </button>
  );
}

export default App;

```
## API Overview
Comprehensive list of methods available on the lyn instance. Most parameters are optional and fall back to default values automatically if omitted.
| Method | Description |
|---|---|
| lyn.log() | Displays a subtle status bar at the bottom of the screen. |
| lyn.info() | Displays an informational modal with title and subtitle. |
| lyn.confirm() | Displays a confirmation modal with callback options. |
| lyn.prompt() | Displays an input modal that resolves a JavaScript Promise. |
| lyn.toast() | Displays a toast notification on the top-right screen. |
| lyn.dynamicIsland() | Displays an expandable Dynamic Island banner. |
| lyn.setLang() | Switches the internal system language ("en" or "id"). |
| lyn.soundNotification() | Enables or disables sound effects for notifications. |
## Detailed API Reference
### lyn.log()
Displays lightweight log bar notifications at the bottom of the viewport.
```javascript
lyn.log({
  Mess: "Request sent successfully, please wait."
});

lyn.log({
  Status: "error",
  Mess: "Failed to connect to server."
});

```
#### Options:
 * Mess *(string, optional)* — The message text content. Defaults to an empty log line.
 * Status *(string, optional)* — Notification state ("default" | "error"). Defaults to "default".
### lyn.info()
Opens a structured modal dialog containing subtitle, title, and detailed message text.
```javascript
lyn.info({
  Subtitle: "Lycaxia Demo",
  Title: "Information",
  Mess: "This is an informational dialog from lyn.info.\nSecond line text is also supported."
});

```
#### Options:
 * Subtitle *(string, optional)* — Header text shown above the main title. Defaults to system localized subtitle.
 * Title *(string, optional)* — Main title text of the modal. Defaults to system localized title.
 * Mess *(string, optional)* — Main message body (supports newlines).
### lyn.confirm()
Displays an interactive confirmation dialog with action callbacks.
```javascript
lyn.confirm({
  Mess: "Are you sure you want to proceed?",
  Event: function() {
    lyn.log({
      Status: "success",
      Mess: "You pressed Continue."
    });
  }
});

```
#### Options:
 * Mess *(string, optional)* — Confirmation prompt message. Defaults to localized confirm text.
 * Event *(function | string, optional)* — Callback function or redirect URL executed when "Continue" is clicked.
### lyn.prompt()
Opens an input modal dialog. Returns a Promise that resolves with user input or rejects if cancelled.
```javascript
async function askNumber() {
  try {
    const number = await lyn.prompt({
      Mess: "Enter your phone number:",
      Type: "num"
    });

    lyn.log({
      Status: "success",
      Mess: "You entered: " + number
    });
  } catch (err) {
    lyn.log({
      Status: "error",
      Mess: "User cancelled the prompt."
    });
  }
}

askNumber();

```
#### Options:
 * Mess *(string, optional)* — Input label prompt text. Defaults to localized prompt title.
 * Type *(string, optional)* — HTML input field type. Defaults to "text".
#### Supported Input Types:
text · number · num · email · url · date · time · tel · range · password
### lyn.toast()
Displays stackable toast notifications at the top-right corner with queued auto-dismissal.
```javascript
lyn.toast({
  Title: "Information",
  Mess: "This is a default toast.",
  Status: "default"
});

lyn.toast({
  Title: "Success",
  Mess: "Data saved successfully.",
  Status: "success"
});

lyn.toast({
  Title: "Error",
  Mess: "Server error occurred.",
  Status: "error"
});

lyn.toast({
  Title: "Permanent",
  Mess: "This toast will not auto-dismiss.",
  Status: "default",
  Permanent: true
});

```
#### Options:
 * Title *(string, optional)* — Toast header title. Defaults to status label or localized text.
 * Mess *(string, optional)* — Toast body text content.
 * Status *(string, optional)* — Toast status theme. Defaults to "default".
 * Permanent *(boolean, optional)* — If true, the toast will stay until closed manually. Defaults to false.
#### Status Values:
default · success · ok · error · err · failed
### lyn.dynamicIsland()
Displays an interactive Dynamic Island banner with smooth expand and collapse animations.
```javascript
lyn.dynamicIsland({
  Status: "success",
  Mess: "File downloaded successfully",
  Label: "download",
  Duration: 3000
});

```
#### Options:
 * Status *(string, optional)* — Defines color accent and status state ("default", "active", "success", "warning", "failed", "waiting"). Defaults to "default".
 * Mess *(string, optional)* — Primary message content.
 * Label *(string, optional)* — Built-in icon and preset type ("home", "notification", "music", "info", "download", "upload", "settings", "success", "failed", "warning", "wait"). Defaults to "info".
 * Duration *(number, optional)* — Display duration in milliseconds.
 * CustomIcon *(string, optional)* — Custom SVG or HTML icon string. Requires Label: "custom".
 * CustomColor *(string, optional)* — Custom icon accent color. Requires Label: "custom".
 * CustomAnimation *(string, optional)* — Custom CSS animation rule. Requires Label: "custom".
#### Custom Icon & Animation Example:
```javascript
lyn.dynamicIsland({
  Label: "custom",
  Mess: "Custom pulse animation!",
  CustomIcon: '<svg viewBox="0 0 24 24"><path d="M12 2a10 10 0 1 0 0 20 10 10 0 0 0 0-20Z"/></svg>',
  CustomColor: "#d0e505",
  CustomAnimation: "lyCustomPulse 1s ease-in-out infinite"
});

```
```css
/* CSS Keyframes in your stylesheet */
@keyframes lyCustomPulse {
  0% { transform: scale(1) rotate(0); }
  50% { transform: scale(1.25) rotate(180deg); }
  100% { transform: scale(1) rotate(360deg); }
}

```
### lyn.setLang()
Switch between supported localization presets.
```javascript
lyn.setLang("en");

lyn.info({
  Mess: "Language is now set to English."
});

lyn.setLang("id");

lyn.info({
  Mess: "Bahasa sekarang menggunakan Indonesia."
});

```
**Supported Languages:** en · id
### lyn.soundNotification()
Controls global sound effects when triggering notifications.
```javascript
// Enable sound
lyn.soundNotification("allow"); // or "on", "enable", "true"

// Disable sound
lyn.soundNotification("off");   // or "false"

```
## Complete Project Example
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Lycaxia Integration</title>
</head>
<body>

  <button onclick="showToast()">Toast</button>
  <button onclick="showConfirm()">Confirm</button>
  <button onclick="showDynamic()">Dynamic Island</button>

  <script src="[https://lib.lycaxia.com/notification/script.js](https://lib.lycaxia.com/notification/script.js)"></script>

  <script>
    lyn.soundNotification("allow");

    function showToast() {
      lyn.toast({
        Title: "Lycaxia",
        Mess: "Hello from Lycaxia!",
        Status: "success"
      });
    }

    function showConfirm() {
      lyn.confirm({
        Mess: "Are you sure you want to proceed?",
        Event: function() {
          lyn.log({
            Status: "success",
            Mess: "Proceeded successfully."
          });
        }
      });
    }

    function showDynamic() {
      lyn.dynamicIsland({
        Status: "success",
        Label: "download",
        Mess: "Download finished!",
        Duration: 3000
      });
    }
  </script>
</body>
</html>

```
## Links & Resources
 * **Official Website:** https://www.lycaxia.com/
 * **Documentation:** https://lib.lycaxia.com/notification/
© Lycaxia 2026.
```
