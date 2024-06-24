# basic_task3_slashproject
To build a weather forecast web application, we need to follow a structured plan. Here is a detailed outline of the project:

1. Setup and Requirements

Frontend: HTML, CSS, JavaScript
Backend: Node.js/Express or Python/Flask/Django (optional for API proxying)
API: OpenWeatherMap or WeatherAPI for fetching weather data

2. Project Structure

Frontend Files:
index.html: Main HTML file
styles.css: Styling file
script.js: JavaScript file for handling API calls and DOM manipulation
Backend Files:
server.js

creating a weather forecast web application involves several steps:
Setting Up the Project: You'll need to create an HTML page, style it with CSS, and add functionality with JavaScript.
Fetching Weather Data: Use an API like OpenWeatherMap to get the weather data.
Handling User Input: Allow the user to input their location.
Auto-detecting Location: Use the Geolocation API to detect the user's location automatically.

#HTML CODE

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather Forecast</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Weather Forecast</h1>
        <input type="text" id="locationInput" placeholder="Enter your location">
        <button onclick="getWeatherByLocation()">Get Weather</button>
        <button onclick="getWeatherByGeolocation()">Detect Location</button>
        <div id="weatherDisplay"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather Forecast</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Weather Forecast</h1>
        <input type="text" id="locationInput" placeholder="Enter your location">
        <button onclick="getWeatherByLocation()">Get Weather</button>
        <button onclick="getWeatherByGeolocation()">Detect Location</button>
        <div id="weatherDisplay"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>
 #CSS CODE
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    text-align: center;
    padding: 50px;
}

.container {
    max-width: 600px;
    margin: auto;
    background: white;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1 {
    margin-bottom: 20px;
}

input, button {
    padding: 10px;
    margin: 10px;
    font-size: 16px;
}

#weatherDisplay {
    margin-top: 20px;
}

#JAVASCRIPT

const apiKey = '1234567abcd';
const weatherDisplay = document.getElementById('weatherDisplay');

function getWeatherByLocation() {
    const location = document.getElementById('locationInput').value;
    if (location) {
        fetchWeatherData(`q=${location}`);
    } else {
        alert('Please enter a location');
    }
}

function getWeatherByGeolocation() {
    if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(position => {
            const { latitude, longitude } = position.coords;
            fetchWeatherData(`lat=${latitude}&lon=${longitude}`);
        }, () => {
            alert('Unable to retrieve your location');
        });
    } else {
        alert('Geolocation is not supported by this browser.');
    }
}

function fetchWeatherData(query) {
    fetch(`https://api.openweathermap.org/data/2.5/forecast?${query}&units=metric&appid=${apiKey}`)
        .then(response => response.json())
        .then(data => {
            if (data.cod === "200") {
                displayWeather(data);
            } else {
                alert('Error: ' + data.message);
            }
        })
        .catch(error => alert('Error: ' + error));
}

function displayWeather(data) {
    weatherDisplay.innerHTML = `
        <h2>Weather Forecast for ${data.city.name}</h2>
        ${data.list.slice(0, 5).map(item => `
            <div>
                <h3>${new Date(item.dt * 1000).toLocaleDateString()}</h3>
                <p>Temperature: ${item.main.temp} °C</p>
                <p>Weather: ${item.weather[0].description}</p>
                <p>Humidity: ${item.main.humidity}%</p>
                <p>Wind Speed: ${item.wind.speed} m/s</p>
            </div>
        `).join('')}
    `;
}


