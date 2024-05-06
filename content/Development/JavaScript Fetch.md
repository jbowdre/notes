---
tags:
  - javascript
  - web
  - api
---
Retrieving data from a web endpoint to display on a static page

```javascript
const wx_endpoint = 'https://paste.jbowdre.lol/tempest.json/raw'; 
// fetch data from pastebin
fetch(wx_endpoint)
  .then(res => res.json())
  .then(function(res){
    // parse data
    let updateTime = res.time;
    let conditions = res.conditions;
    let temp = res.temperature;
    let humidity = res.humidity;
    let wind = res.wind_gust;
    let rainToday = res.rain_today;
    let pressure = res.pressure;

    // display data
    document.getElementById('time').innerHTML = updateTime;
    document.getElementById('conditions').innerHTML = conditions;
    document.getElementById('temp').innerHTML = temp;
    document.getElementById('humidity').innerHTML = humidity;
    document.getElementById('wind').innerHTML = wind;
    document.getElementById('rainToday').innerHTML = rainToday;
    document.getElementById('pressure').innerHTML = pressure;
  });

```

More @[runtimeterror](https://runtimeterror.dev/display-tempest-weather-static-site/)