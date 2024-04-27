# weatherApp
weather website developed using html Javascriprt CSS

//   HTML code (Javascript also used)  //

<!DOCTYPE html>
<html>
    <head>
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Weather App</title>
        <link rel="stylesheet" href="style.css">
    </head>
    <body>
        <div class="card">
            <div class="search">
                <input type="text" placeholder="enter city name"
                    spellcheck="false">
                <button><img
                        src="https://e7.pngegg.com/pngimages/770/106/png-clipart-computer-icons-search-box-magnifying-glass-search-for-miscellaneous-desktop-wallpaper-thumbnail.png"></button>
            </div>
           <div class="error">
            <p>Invalid city name</p>
           </div>
            <div class="weather">
                <img
                    src="https://www.freepnglogos.com/uploads/rain-png/transparent-download-green-cloud-with-rain-clipart-png-23.png"
                    class="weather-icon">
                <h1 class="temp">22°C</h1>
                <h2 class="city">New York</h2>
                <div class="details">
                    <div class="col">
                        <img
                            src="https://cdn-icons-png.flaticon.com/512/3262/3262966.png">
                        <div>
                            <p class="humidity">50%</p>
                            <p>Humidity</p>
                        </div>
                        <div class="col">
                            <img
                                src="https://w7.pngwing.com/pngs/659/622/png-transparent-smoke-wind-cloud-wind-blue-text-logo-thumbnail.png">
                            <div>
                                <p class="wind">15 km/h</p>
                                <p>Wind speed</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <script>
      const apiKey ="bd5641b4ade59e9c9e7f343ad1b66aba      ";
      const apiUrl ="https://api.openweathermap.org/data/2.5/weather?units=metric&q=";

      const searchBox = document.querySelector(".search input");
      const searchBtn = document.querySelector(".search button");
      const weatherIcon = document.querySelector(".weather-icon");


      async function checkWeather(city){
        const response = await fetch(apiUrl + city + `&appid=${apiKey}`);

        if(response.status == 404){
            document.querySelector(".error").style.display = "block";
            document.querySelector(".weather").style.display = "none";
            }
        else{var data = await response.json();
       


            document.querySelector(".city").innerHTML = data.name;
            document.querySelector(".temp").innerHTML = Math.round(data.main.temp) + "°C";
            document.querySelector(".humidity").innerHTML = data.main.humidity + "%";
            document.querySelector(".wind").innerHTML = data.wind.speed + "km/h";
    
            
            if(data.weather[0].main == "Clear"){
                weatherIcon.src ="https://toppng.com/uploads/preview/ood-environment-11563166135rz6peg1pfo.png";
            }
            else if(data.weather[0].main == "Rain"){
                weatherIcon.src ="https://www.freepnglogos.com/uploads/rain-png/transparent-download-green-cloud-with-rain-clipart-png-23.png";
            }
            else if(data.weather[0].main == "Drizzle"){
                weatherIcon.src ="https://png.pngtree.com/png-vector/20201128/ourmid/pngtree-drizzling-clouds-png-image_2480510.jpg";
            }
            else if(data.weather[0].main == "Mist"){
                weatherIcon.src ="https://thumbs.dreamstime.com/b/fog-smoke-isolated-transparent-special-effect-white-vector-cloudiness-mist-smog-background-png-fog-smoke-isolated-210129290.jpg";
            }
            else if(data.weather[0].main == "Clouds"){
                weatherIcon.src = "https://png.pngtree.com/png-vector/20210805/ourmid/pngtree-3d-cloud-illustration-vector-png-image_3780086.jpg";
            }
            document.querySelector(".weather").style.display = "block";
            document.querySelector(".error").style.display = "none";
        }   

    }

        
            searchBtn.addEventListener("click", ()=>{
                checkWeather(searchBox.value);
              })

        
    
 


    </script>
        </body>
    </html>

// CSS link to the code is //

*{
    margin: 0;
    padding: 0;
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    box-sizing: border-box;
}
body{
    background: #222;
}
.card{
    width: 90%;
    max-width: 470px;
    background: linear-gradient(135deg, #00feba, #5b5b5b);
    color: #fff;
    margin: 100px auto 0;
    border-radius: 20px;
    padding: 40px 35px;
    text-align: center;
}
.search{
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.search input{
    border: 0;
    outline: 0;
    background: #ebfffc;
    color: #555;
    padding: 10px 25px;
    height: 60px;
    border-radius: 30pcx;
    flex: 1;
    margin-right: 16px;
    font-size: 18px;
}
.search button{
    border: 0;
    outline: 0;
    background: #ebfffc;
    border-radius: 50%;
    width: 60px;
    height: 60px;
    cursor: pointer;
}
.search button img{
    width: 16px;
}
.weather-icon{
    width: 170px;
    margin-top: 30px;
}
.weather h1{
    font-size: 80px;
    font-weight: 500;
}
.weather h2{
    font-size: 45px;
    font-weight: 400;
    margin-top: -10px;
}
.details{
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 20px;
    margin-top: 50px;
}
.col{
    display: flex;
    align-items: center;
    text-align: left;
}
.col img{
    width: 40px;
    margin-right: 10px;
}
.humidity, .wind{
    font-size: 28px;
    margin-top: -6px;
}
.weather{
    display: none;
}
.error{
    text-align: left;
    margin-left: 10px;
    font-size: 14px;
    margin-top: 10px;
    display: none;
}
