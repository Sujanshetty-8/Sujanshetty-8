# Browser Sensor Data Collector

This project provides a simple, modern web frontend designed to collect sensor data directly from the user's browser, assign a unique identifier to each browser instance, and send this data, along with timestamps, to a specified backend endpoint at a user-defined interval.

It's built with standard web technologies (HTML, CSS, JavaScript) and utilizes Web APIs for sensor access.

---

## Features

* **Unique Browser ID Generation**: Automatically generates and stores a unique ID for each browser instance using `localStorage`, ensuring consistent tracking across sessions.
* **Geolocation Data Collection**: Reads latitude, longitude, and accuracy using the Geolocation API.
* **Ambient Light Data Collection**: Gathers ambient light intensity (illuminance in lux) via the Ambient Light Sensor API.
* **Customizable Collection Interval**: Users can select the data collection frequency (1, 2, 5, 10, 30, or 60 seconds) using a dropdown.
* **Start/Stop Controls**: Dedicated buttons to easily begin and cease data collection.
* **Real-time Display**: Shows collected sensor data in a neatly formatted table on the frontend, updated with each reading.
* **Backend Integration**: Sends collected data (unique ID, timestamp, sensor readings) as a JSON payload to a configurable backend endpoint.
* **Attractive UI**: Features a clean design with hover effects on buttons for a better user experience.

---

## Getting Started

Follow these steps to get the project up and running on your local machine.

### Prerequisites

* A modern web browser (e.g., Chrome, Firefox, Edge, Safari) that supports Geolocation API and Ambient Light Sensor API.
* **HTTPS (Highly Recommended)**: Many browser sensor APIs, including the Ambient Light Sensor, require a **secure context (HTTPS)** to function. If you open `index.html` directly from your file system (`file://` URL), sensor data might not be accessible, or you may encounter repeated permission prompts. For full functionality, serve the files using a local web server (see below).

### Installation

1.  **Clone the Repository (or Download):**
    ```bash
    git clone [https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git](https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git)
    cd YOUR_REPOSITORY_NAME
    ```
    (Replace `YOUR_USERNAME` and `YOUR_REPOSITORY_NAME` with your actual GitHub details.)

2.  **Navigate to the Project Directory:**
    Ensure you are in the folder containing `index.html`, `style.css`, and `script.js`.

---

## Usage

### 1. Configure Your Backend Endpoint

Open `script.js` and find the `sendDataToBackend` function. Replace `'YOUR_BACKEND_ENDPOINT_HERE'` with the actual URL of your backend server where you want to send the sensor data.

```javascript
// script.js
async function sendDataToBackend(data) {
    const backendUrl = '[https://your-actual-backend-api.com/sensor-data](https://your-actual-backend-api.com/sensor-data)'; // <--- CHANGE THIS
    // ... rest of the function
}
2. Run Locally (Recommended via Web Server)
To ensure all sensor APIs function correctly, especially the Ambient Light Sensor, it's best to serve the files using a simple local HTTP server.

Using Python's Simple HTTP Server:
If you have Python installed, navigate to your project directory in the terminal and run:

Bash

python -m http.server 8000
Then, open your browser and go to http://localhost:8000.

Using Node.js http-server (if you have Node.js):
Install http-server globally:

Bash

npm install -g http-server
Navigate to your project directory in the terminal and run:

Bash

http-server -p 8000 -S
The -S flag enables HTTPS, which is crucial for some sensor APIs. You might get
a certificate warning, which you can usually bypass for local development.
Then, open your browser and go to https://localhost:8000.

3. Using the Frontend
Once the page loads, you'll see a Unique Browser Instance ID. This ID is unique to your browser and will persist across sessions.

Select your desired Collection Interval (in seconds) from the dropdown.

Click the "Start Collection" button.

Your browser will likely prompt you for permissions to access your Geolocation
and potentially the Ambient Light Sensor. Grant these permissions for
data collection to proceed.

The table will start populating with new sensor readings at your chosen interval.

Messages indicating successful or failed backend data sends will briefly appear in the table.

Click the "Stop Collection" button to halt data gathering.

Sensor Data Payload Format
The data sent to your backend will be a JSON object with the following structure:

JSON

{
    "timestamp": "2025-07-24T16:00:00.000Z", // ISO 8601 format
    "browserInstanceId": "xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx",
    "geolocation": {
        "latitude": 12.9716,
        "longitude": 77.5946,
        "accuracy": 15.0, // in meters
        "error": null    // or an error message if geolocation failed
    },
    "ambientLight": {
        "illuminance": 150.75, // in lux
        "error": null          // or an error message if ambient light reading failed or not supported
    }
}
If a sensor is not supported by the browser or permission is denied,
its corresponding error field will contain a descriptive message,
and the data fields will be null or 'N/A'.
