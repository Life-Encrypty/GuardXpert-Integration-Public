
# Event Listeners Script (`event-listeners.js`) Documentation

This documentation explains how to use the `event-listeners.js` script to track and log events from Shaka Player and HTML5 video elements. This script helps monitor various playback activities and can be extended to handle custom actions when events occur.

## Prerequisites

- You must use **release V0.4.1 or later** to ensure compatibility with this script.
- You must import the script at the end of scripts.

## Usage

1. **Include the Script in Your HTML File:**

   To use the `event-listeners.js` script, make sure it is included after the Shaka Player library and your player configuration script:

   ```html
   <!-- Include the event listeners script -->
   <script src="https://GuardXpert.b-cdn.net/libs/v0.4.1/event-listeners.js"></script>
   ```

2. **Log Playback Events:**

   The `event-listeners.js` script automatically logs various events related to HTML5 video and Shaka Player. A log container (`logContainer`) is dynamically created and appended to the body, displaying messages such as "Playback started", "Shaka Player content loaded", etc.

## Development Note

### Logging Code for Development Only

The following part of the script is intended for development purposes to help debug and monitor events during the development phase. **This code should be removed or disabled in production** to avoid performance impacts and potential exposure of sensitive information.

```javascript
// Create a div element for logs
const logContainer = document.createElement('div');
logContainer.id = 'logContainer';
logContainer.style.marginTop = '20px';
logContainer.style.maxHeight = '200px';
logContainer.style.overflowY = 'auto';
logContainer.style.backgroundColor = '#f0f0f0';
logContainer.style.border = '1px solid #ddd';
logContainer.style.padding = '10px';
logContainer.style.fontSize = '12px';
logContainer.style.color = '#333';
logContainer.style.fontFamily = 'monospace';

// Append the container div to the body
document.body.appendChild(logContainer);

// Function to log messages to the log container
function logMessage(message) {
  // Get the log container by its ID
  const logContainer = document.getElementById('logContainer');

  if (logContainer) {
    const logEntry = document.createElement('div');
    logEntry.textContent = message;
    logContainer.appendChild(logEntry);
    logContainer.scrollTop = logContainer.scrollHeight; // Auto-scroll to the latest message
  } else {
    console.error('Log container not found!');
  }
}
```

## How to Extend the Script


### 1. Customize the `logMessage` Function

Modify the `logMessage` function to perform more complex logging operations or to trigger additional actions:

```javascript
function logMessage(message) {
  const logContainer = document.getElementById('logContainer');

  if (logContainer) {
    const logEntry = document.createElement('div');
    logEntry.textContent = message;
    logContainer.appendChild(logEntry);
    logContainer.scrollTop = logContainer.scrollHeight; // Auto-scroll to latest message

    // Example: Send logs to an external server
    sendLogToServer(message);
  } else {
    console.error('Log container not found!');
  }
}

function sendLogToServer(message) {
  fetch('/log', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ log: message })
  });
}
```

### 2. Handle Specific Player Actions

The script can be extended to perform specific actions when certain events occur. For example, you can change the appearance of the video player when buffering:

```javascript
player.addEventListener('buffering', (event) => {
  logMessage(`Shaka Player buffering: ${event.buffering}`);
  if (event.buffering) {
    // Custom action when buffering starts
    document.getElementById('my-player').classList.add('buffering');
  } else {
    // Custom action when buffering ends
    document.getElementById('my-player').classList.remove('buffering');
  }
});
```

## Key Features

- **Dynamic Event Logging**: Automatically logs a wide range of playback events.
- **Easy Customization**: Easily add new event listeners or modify the log message function to handle more complex scenarios.
- **Extensible**: Use the script as a base to build more advanced features, such as sending logs to a server, updating the UI dynamically, or handling custom events.

## Conclusion

The `event-listeners.js` script is a powerful tool for monitoring Shaka Player and HTML5 video events. It can be easily extended to meet custom needs, providing flexibility and control over playback behavior.

Feel free to experiment by adding new event listeners or enhancing the `logMessage` function to create a more robust and feature-rich logging system.
