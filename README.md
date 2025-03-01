<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <style>
        h1{
            color: #f7f7f7;
            font-family:'Times New Roman', Times, serif'
        }
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #264968;
            padding: 20px;
    
                background-image: url('weather.jpg');
                background-size: cover,contain;
                background-position: center;
                background-repeat: no-repeat;
        }
        .container {
            max-width: 400px;
            margin: auto;
            background: rgb(129, 152, 214);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        }
        input, button {
            margin: 10px 0;
            padding: 10px;
            width: 80%;
        }
        button {
            background-color: #d9e445;
            color: rgb(247, 30, 14);
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #7eac73;
        }
        .weather-info {
            margin-top: 20px;
        }
        .weather-icon {
            width: 100px;
            height: 100px;
            margin: 10px auto;
        }
        
    </style>
</head>
<body>
    <h1 text-algin="center">You can predict weather status here</h1>
    <div class="container">
        <h2>Weather App</h2>
        <input type="text" id="location" placeholder="Enter location" />
        <button onclick="getWeather()">Get Weather</button>
        <div class="weather-info" id="weather-info"></div>
    </div>

    <script>
        async function getWeather() {
            const location = document.getElementById("location").value;
            if (!location) {
                alert("Please enter a location");
                return;
            }
            
            const apiKey = "da6c893e1fec44508fe91221250103";
            const url = `http://api.weatherapi.com/v1/current.json?key=${apiKey}&q=${location}&aqi=yes`;
            
            try {
                const response = await fetch(url);
                const data = await response.json();
                
                if (data.error) {
                    document.getElementById("weather-info").innerHTML = `<p>${data.error.message}</p>`;
                } else {
                    document.getElementById("weather-info").innerHTML = `
                        <h3>${data.location.name}, ${data.location.country}</h3>
                        <img class="weather-icon" src="${data.current.condition.icon}" alt="Weather Icon">
                        <p>Temperature: ${data.current.temp_c}°C</p>
                        <p>Wind Speed: ${data.current.wind_kph} kph</p>
                        <p>Cloud Cover: ${data.current.cloud}%</p>
                    `;
                }
            } catch (error) {
                document.getElementById("weather-info").innerHTML = `<p>Failed to fetch weather data. Please try again.</p>`;
            }
        }
    </script>
</body>
</html>
