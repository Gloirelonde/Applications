# Applicationsconst row = document.querySelector('.row')
const titre = document.querySelector('.titre')
console.log(axios);

var config = {
    method: "get",
    url: "https://api.openweathermap.org/data/2.5/forecast?lat=5.320357&lon=-4.016107&units=metric&lang=fr&appid=775b43c6cfc7dcb4ef93f452147deda1",
    headers: {},
};

axios(config)
    .then(function (response) {
        //   console.log(JSON.stringify(response.data));
        var data = response.data;
        console.log(data)
        var dataList = data.list;
        
        var titreText = data.city.name
        titre.innerHTML = `Météo ${titreText}`

        dataList.forEach(element => {
            var temp = element.main.temp
            var feels_like = element.main.feels_like
            var icon = element.weather[0].icon
            var desc = element.weather[0].description
            var humidity = element.main.humidity
            var wind = element.wind.speed
            var date = element.dt

            date = new Date(date * 1000).toLocaleString()

            row.innerHTML += `
            <div class="col-md-3 mb-5">
                <div class="col-md-12">
                    <div class="card">
                        <img src="http://openweathermap.org/img/wn/${icon}@2x.png" class="card-img-top mx-auto mw-100" style="width: 200px">
                        <h5 class="card-title text-info">${desc}</h5>
                        <div class="card-body">
                            <h5 class="card-title text-secondary">${date}</h5>
                            <h2 class="card-title">${temp}°C</h4>
                            <h6 class="card-title text-muted">Résentir: ${feels_like}°C</h6>
                            <h6 class="card-title text-muted">Humidité: ${humidity}%</h6>
                            <h6 class="card-title text-muted">Vitesse du vent: ${wind}%</h6>
                        </div>
                    </div>
                </div>
            </div>
            `
            console.log(element)
        });
    })
    .catch(function (error) {
        console.log(error);
    });
