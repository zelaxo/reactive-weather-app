<script>
    //Variables
    let city = 'Mumbai';
    let country = 'IN';
    let query = 'mumbai';
    let weather = 'Clouds';
    let humidity = '57';
    let pressure = '1011';
    let wind = '3.87';
    let uv = '0';
    let temp = '30';
    let temp1 = '30';
    let temp2 = '30';
    let temp3 = '30';
    let temp4 = '30';
    let date = moment().format('MMMM Do YYYY');
    let day = moment();
    let population = 1000000;
    //End Of Variables

    //Functions

    //Call on first invoke
    $:axios.get(`https://api.openweathermap.org/data/2.5/forecast?q=${query}&mode=json&appid=44778f4f75d655331587deddb616b931`).then((result) => {
            city = result.data.city.name;
            population = result.data.city.population;
            country = result.data.city.country;
            temp = (Math.round((result.data.list[0].main.temp - 273.15)*100/100)).toString();
            weather = result.data.list[0].weather[0].main;
            wind = result.data.list[0].wind.speed;
            pressure = result.data.list[0].main.pressure;
            humidity = result.data.list[0].main.humidity;
            temp1 = (Math.round((result.data.list[1].main.temp - 273.15)*100/100)).toString();
            temp2 = (Math.round((result.data.list[2].main.temp - 273.15)*100/100)).toString();
            temp3 = (Math.round((result.data.list[3].main.temp - 273.15)*100/100)).toString();
            temp4 = (Math.round((result.data.list[4].main.temp - 273.15)*100/100)).toString();
        }).catch((err) => console.log(err));

    //Fetch new values every 10 minutes
    $:setTimeout(function() {
        axios.get(`https://api.openweathermap.org/data/2.5/forecast?q=${query}&mode=json&appid=44778f4f75d655331587deddb616b931`).then((result) => {
            city = result.data.city.name;
            population = result.data.city.population;
            country = result.data.city.country;
            temp = (Math.round((result.data.list[0].main.temp - 273.15)*100/100)).toString();
            weather = result.data.list[0].weather[0].main;
            wind = result.data.list[0].wind.speed;
            pressure = result.data.list[0].main.pressure;
            humidity = result.data.list[0].main.humidity;
            temp1 = (Math.round((result.data.list[1].main.temp - 273.15)*100/100)).toString();
            temp2 = (Math.round((result.data.list[2].main.temp - 273.15)*100/100)).toString();
            temp3 = (Math.round((result.data.list[3].main.temp - 273.15)*100/100)).toString();
            temp4 = (Math.round((result.data.list[4].main.temp - 273.15)*100/100)).toString();
        }).catch((err) => console.log(err));
    }, 600000);

    //Make a call on clicking search
    function search() {
        axios.get(`https://api.openweathermap.org/data/2.5/forecast?q=${query}&mode=json&appid=44778f4f75d655331587deddb616b931`).then((result) => {
            city = result.data.city.name;
            population = result.data.city.population;
            country = result.data.city.country;
            temp = (Math.round((result.data.list[0].main.temp - 273.15)*100/100)).toString();
            weather = result.data.list[0].weather[0].main;
            wind = result.data.list[0].wind.speed;
            pressure = result.data.list[0].main.pressure;
            humidity = result.data.list[0].main.humidity;
            temp1 = (Math.round((result.data.list[1].main.temp - 273.15)*100/100)).toString();
            temp2 = (Math.round((result.data.list[2].main.temp - 273.15)*100/100)).toString();
            temp3 = (Math.round((result.data.list[3].main.temp - 273.15)*100/100)).toString();
            temp4 = (Math.round((result.data.list[4].main.temp - 273.15)*100/100)).toString();
        }).catch((err) => window.alert('City not found!'));
    }

    //Updating Date & Day
    $:setTimeout(function() {
        date = moment().format('MMMM Do YYYY');
        day = moment();
    }, 600000);

    //Calculating next 4 days
    $:day1 = moment(day).add(1, 'days');
    $:day2 = moment(day1).add(1, 'days');
    $:day3 = moment(day2).add(1, 'days');
    $:day4 = moment(day3).add(1, 'days');

    //Representing date in a suitable format
    $:day1show = day1.format('MMM D');
    $:day2show = day2.format('MMM D');
    $:day3show = day3.format('MMM D');
    $:day4show = day4.format('MMM D');

</script>

<!-- Markup -->
    <div style="padding-right:20px; padding-left:20px; padding-bottom:20px;">

    <div class="row shadow mt-100">
        <div class="column2" style="background-image: url(images/gif/{weather}.gif); background-repeat: no-repeat; background-size: cover;">
            <table width="100%" style="padding:10px;">
                <tr>
                    <td width="70%" >
                        <h2 class="font-weight-700 text-color-white lh-80">{city}<br>
                        <span class="font-weight-400 fs-15">{country}</span></h2>
                    </td>
                    <td width="30%">
                        <div class="search">
                            <input type="text" class="searchTerm" placeholder="Search" bind:value={query}>
                            <button type="submit" class="searchButton" on:click ={search}>
                                <img alt="Search" src="images/icon/search.svg" class="">
                            </button>
                        </div>
                    </td>
                </tr>
                <tr>
                    <td>
                        <span class="tempfont">{temp}° C</span>
                        <p class="text-color-white">{weather}<br>
                        {date}</p>
                    </td>
                    <td>
                        <img src="images/weather/light/{weather}.png" class="weaicon" alt="weather">
                    </td>
                </tr>
            </table>
        </div>
        <div class="column" style="background-color:#ededed;">
            <div style="background-color: #191919; color: white; padding: 15px; border-radius: 10px;">
                <table width="100%">
                    <tr>
                        <td width="50%">
                            <img src="images/weather/humidity.png" height="20" alt="Humidity">
                            <p>Humidity</p>
                        </td>
                        <td width="50%">
                            <p Align="right" class="fs-30 lh-5">{humidity}%</p>
                        </td>
                    </tr>
                </table>
            </div>
            <div style="background-color: #191919; color: white; padding: 15px; border-radius: 10px; margin-top: 10px;">
                <table width="100%">
                    <tr>
                        <td width="50%">
                            <img src="images/weather/light/storm.png" height="20" alt="Wind">
                            <p>Wind</p>
                        </td>
                        <td width="50%">
                            <p Align="right" class="fs-30 lh-5">{wind} mps</p>
                        </td>
                    </tr>
                </table>
            </div>
            <div style="background-color: #191919; color: white; padding: 15px; border-radius: 10px; margin-top: 10px;">
                <table width="100%">
                    <tr>
                        <td width="50%">
                            <img src="images/weather/pressure.png" height="20" alt="Pressure">
                            <p>Pressure</p>
                        </td>
                        <td width="50%">
                            <p Align="right" class="fs-30 lh-5">{pressure} hPa</p>
                        </td>
                    </tr>
                </table>
            </div>
            <div style="background-color: #191919; color: white; padding: 15px; border-radius: 10px; margin-top: 10px;">
                <table width="100%">
                    <tr>
                        <td width="50%">
                            <img src="images/weather/people.png" height="20" alt="uv">
                            <p>Population</p>
                        </td>
                        <td width="50%">
                            <p Align="right" class="fs-30 lh-5">{population}</p>
                        </td>
                    </tr>
                </table>
            </div>
        </div>
        <div class="column3" style="background-color:#ededed;">
            <div style="background-color: #191919; color: white; padding: 30px; border-radius: 10px;">
                <h3>4 DAY FORCAST</h3>
                <table width="100%">
                    <tr>
                        <td width="20%" style="padding: 5px;">
                            <div class="card" Align="center">
                                <p class="fs-30">{temp1}° <span class="text-color-grey fs-20">C</span></p>
                                <img src="images/weather/light/cold.png" alt="Icon" height="50" class="m-50">
                                <p class="fs-20">{day1show}</p>
                            </div>
                        </td>
                        <td width="20%" style="padding: 5px;">
                            <div class="card" Align="center">
                                <p class="fs-30">{temp2}° <span class="text-color-grey fs-20">C</span></p>
                                <img src="images/weather/light/cold.png" alt="Icon" height="50" class="m-50">
                                <p class="fs-20">{day2show}</p>
                            </div>
                        </td>
                        <td width="20%" style="padding: 5px;">
                            <div class="card" Align="center">
                                <p class="fs-30">{temp3}° <span class="text-color-grey fs-20">C</span></p>
                                <img src="images/weather/light/cold.png" alt="Icon" height="50" class="m-50">
                                <p class="fs-20">{day3show}</p>
                            </div>
                        </td>
                        <td width="20%" style="padding: 5px;">
                            <div class="card" Align="center">
                                <p class="fs-30">{temp4}° <span class="text-color-grey fs-20">C</span></p>
                                <img src="images/weather/light/cold.png" alt="Icon" height="50" class="m-50">
                                <p class="fs-20">{day4show}</p>
                            </div>
                        </td>
                    </tr>
                </table>
            </div>
        </div>
    </div>
    <br><br>
    <!-- Credits -->
    <div style="text-align:center;color:white">
        <h5>POWERED BY OPENWEATHERMAP</h5>
    </div>
    </div>