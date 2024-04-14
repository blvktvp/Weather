<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App - by Raju Webdev</title>
    <link rel="icon" type="image/x-icon" href="/Images/favicon.png">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.2/css/all.min.css"
        integrity="sha512-1sCRPdkRXhBV2PBLUdRb4tMg1w2YPf37qatUFeS7zlBy7jJI8Lf4VHwWfZZfpXtYSLy85pkm9GaYVYMfw5BC1A=="
        crossorigin="anonymous" referrerpolicy="no-referrer" />
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@500&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <!-- Main Container for the weather web app -->
    <div class="weatherContainer">
        <h2 class="appHeading"> Weather App </h2>
        <!-- Input Divition for city name -->
        <div class="search">
            <form action="" id="weatherForm">
                <input type="text" name="" id="weatherInput" placeholder="Enter your city here...">
                <button class="searchBtn" type="submit">
                    <ul>
                        <li><i class="fa-solid fa-magnifying-glass"></i></li>
                    </ul>
                </button>
            </form>
        </div>
        <!-- Outut Will show on the screen -->
        <h2 id="city"></h2>
        <img src="." alt="" id="weatherImage">
        <p class="weatherMain" id="weatherMain"></p>
        <h2 id="temp"><span class="temp"></span></h2>
        <div class="todayDates"></div>
        <div id="todayTime"></div>
    </div>
</body>
<script src="script.js"></script>

</html>



* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #202b33;
}

.weatherContainer {
  margin: 2rem;
  padding: 2rem 1rem;
  border-radius: 1rem;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  box-shadow: 0px 0px 19px 0px #18bd9e;
  color: #f0ce0e;
  color: #86d3d3 #494bcf #a58d3e #e6cdd7;
}

#weatherForm input {
  border: none;
  color: rgb(0, 0, 0);
  outline: none;
  font-size: 1rem;
  font-family: sans-serif;
  background: transparent;
}

#weatherForm ul li {
  list-style: none;
}

.searchBtn {
  background: transparent;
  border: none;
}

.searchBtn ul li {
  list-style: none;
  font-size: 1.2rem;
}

#weatherForm {
  display: flex;
  justify-content: space-around;
}

.appHeading {
  text-align: center;
  margin-bottom: 1rem;
  font-family: 'Poppins', sans-serif;
}

#city {
  text-transform: capitalize;
  text-align: center;
  margin-top: 1rem;
  font-family: 'Poppins', sans-serif;
}

.weatherContainer img {
  width: 50%;
}

#temp {
  word-spacing: -8px;
  font-size: 2.5rem;
  margin-bottom: 1rem;
  font-family: 'Poppins', sans-serif;
}

#temp sup {
  font-size: 1.5rem;
}

.weatherMain {
  font-family: sans-serif;
}

#todayTime,
.todayDates {
  font-family: sans-serif;
  line-height: 2rem;
}


/* Utility Classes */
.d-flex {
  display: flex;
}

.justify-space-around {
  justify-content: space-around;
}

.justify-space-center {
  justify-content: center;
}

.align-items-center {
  align-items: center;
}

.f-col {
  flex-direction: column;
}

/* Media Query for Responsive */
@media screen and (max-width: 307px) {
  #weatherForm {
      flex-direction: column;
  }

  #weatherForm input {
      text-align: center;
      margin-bottom: 1rem;
  }
}



// Variabless
const cityName = document.querySelector('#weatherInput');
const searchBtn = document.querySelector('#searchBtn');
const form = document.getElementById('weatherForm');
const myCity = document.getElementById('city');
const image = document.getElementById('weatherImage');
const weather = document.getElementById('weatherMain');
const temp = document.querySelector('.temp');
const dates = document.querySelector('.todayDates');
const times = document.getElementById('todayTime');
let date = new Date();

// Function work when user input the city name
form.addEventListener('submit', function (e) {

    // preventDefault() to stop page reload
    e.preventDefault();

    // Updating the city name
    let city = cityName.value;
    const myWeatherContainer = document.querySelector('.weatherContainer');
    const apiID = `931f131dde3f4ae2fcbc3289fc646471`;
    // API URL
    let url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${apiID}`

    // fetching data from the weather api
    fetch(url).then((response) => {
        return response.json();
    }).then((data) => {

        const tempValue = Math.round(data['main']['temp']);
        const weatherMain = data['weather'][0]['main'];
        weather.innerHTML = weatherMain;

        // Updating the DOM
        myCity.innerHTML = city;
        temp.innerHTML = `${tempValue}`
        weather.innerHTML = `${weatherMain}`
        temp.innerHTML = `${tempValue}<span><sup>o</sup>C</span.`;

        // Updating the Images according to the weather
        if (weatherMain == 'Clear') {
            image.src = `./Images/sunny.png`
            myWeatherContainer.style.backgroundColor = '#f0ce0e'
        }
        if (weatherMain == 'Clouds') {
            image.src = `./Images/clouds.png`
            myWeatherContainer.style.backgroundColor = '#86d3d3'
        }
        if (weatherMain == 'Rain') {
            image.src = `./Images/Rain.png`
            myWeatherContainer.style.backgroundColor = '#494bcf'
        }
        if (weatherMain == 'Drizzle') {
            image.src = `./Images/Drizzle.png`
            myWeatherContainer.style.backgroundColor = '#a58d3e'
        }
        if (weatherMain == 'Haze') {
            image.src = `./Images/Drizzle.png`
            myWeatherContainer.style.backgroundColor = '#e6cdd7'
        }

        // Updating dates
        const currentMonth = date.getMonth();
        switch (currentMonth) {
            case 0:
                dates.innerHTML = `${date.getDate()}, Jan`
                break;
            case 1:
                dates.innerHTML = `${date.getDate()}, Feb`
                break;
            case 2:
                dates.innerHTML = `${date.getDate()}, Mar`
                break;
            case 3:
                dates.innerHTML = `${date.getDate()}, Apr`
                break;
            case 4:
                dates.innerHTML = `${date.getDate()}, May`
                break;
            case 5:
                dates.innerHTML = `${date.getDate()}, Jun`
                break;
            case 6:
                dates.innerHTML = `${date.getDate()}, Jul`
                break;
            case 7:
                dates.innerHTML = `${date.getDate()}, Aug`
                break;
            case 8:
                dates.innerHTML = `${date.getDate()}, Sept.`
                break;
            case 9:
                dates.innerHTML = `${date.getDate()}, Oct.`
                break;
            case 10:
                dates.innerHTML = `${date.getDate()}, Nov`
                break;
            case 11:
                dates.innerHTML = `${date.getDate()}, Dec`
                break;
        }

        // Updating times       
        function leftInterval() {
            const left = document.getElementById('todayTime')
            let leftDate = new Date();
            let hours = leftDate.getHours();
            let minutes = leftDate.getMinutes();
            let seconds = leftDate.getSeconds();

            if (hours == 0) {
                hours = 12;
            }

            if (hours > 12) {
                hours = hours - 12;
            }
            left.innerHTML = `${hours}h: ${minutes}m: ${seconds}s`
        }
        setInterval(leftInterval, 1000);
    })
})
