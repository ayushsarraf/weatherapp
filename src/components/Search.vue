<template>
  <div>
    <div class="col-xs-12 col-sm-12 text-center">
      <h1 class="heading">
        Weather
        <i class="fab fa-cloudversify"></i>
      </h1>

      <div class="d-flex justify-content-center">
        <input
          type="text"
          class="form-control text-center"
          placeholder="Enter City"
          id="search-box"
          required
          v-model="enteredCity"
        />
        <button class="btn btn-primary search-btn" @click="fetchWeather">Search</button>
      </div>
    </div>
    <div class="col-xs-12 col-sm-12 text-center current">
      <h2>{{date}}</h2>
      <h6>{{currentCity}}, {{countryCode}}</h6>
    </div>
    <div class="d-flex justify-content-center weather-degree">
      <img :src="img" />
      <h5 class="text-center degree">
        {{temp}}
        <br />
        {{dayInfo}}
      </h5>
    </div>
  </div>
</template>


<script>
import axios from "axios";
import { eventBus } from "../main";
export default {
  data: function () {
    return {
      API: "d1e7aa1822b6e06dbb846a76737fc23e",
      enteredCity: "",
      date: date(),
      currentCity: "---",
      countryCode: "---",
      temp: "",
      dayInfo: "---",
      img: "http://openweathermap.org/img/wn/10d@2x.png",
      link:
        "https://api.openweathermap.org/data/2.5/weather?q=ranchi&units=metric&appid=d1e7aa1822b6e06dbb846a76737fc23e",
      otherdata: {
        high: "",
        wind: "",
        humidity: "",
        info: "",
      },
    };
  },
  methods: {
    fetchWeather() {
      var apiLink =
        "https://api.openweathermap.org/data/2.5/weather?q=" +
        this.enteredCity +
        "&units=metric&appid=d1e7aa1822b6e06dbb846a76737fc23e";

      if (this.enteredCity != "")
        axios
          .get(apiLink)
          .then((response) => this.show(response.data))
          .catch((err) => {
            console.log(err);

            this.temp = "----";
            this.countryCode = "----";
            this.currentCity = "----";
            this.dayInfo = "----";
            this.img = "----";
            this.otherdata.high ="----";
            this.otherdata.wind = "----";
            this.otherdata.humidity = "----";
            this.otherdata.info = "----";
             eventBus.$emit("newData", this.otherdata);
          });
    },
    show(weather) {
      this.temp = weather.main.temp + "°C";
      this.countryCode = weather.sys.country;
      this.currentCity = weather.name;
      this.dayInfo = weather.weather[0].description;
      this.img =
        "http://openweathermap.org/img/wn/" +
        weather.weather[0].icon +
        "@2x.png";
      this.otherdata.high =
        weather.main.temp_max + "°C/" + weather.main.temp_min + "°C";
      this.otherdata.wind = weather.wind.speed;
      this.otherdata.humidity = weather.main.humidity;
      console.log(weather.main.humidity);
      this.otherdata.info = weather.visibility;
      eventBus.$emit("newData", this.otherdata);
      console.log(weather);
      this.enteredCity = "";
    },
    setData() {},
  },
};

function date() {
  var today = new Date();
  var dd = String(today.getDate()).padStart(2, "0");
  var mm = String(today.getMonth() + 1).padStart(2, "0"); //January is 0!
  var yyyy = today.getFullYear();

  today = getMonth(mm) + " " + dd + ", " + yyyy;

  return today;
}

function getMonth(month) {
  var months = [
    "Jan",
    "Feb",
    "Mar",
    "Apr",
    "May",
    "Jun",
    "Jul",
    "Aug",
    "Sep",
    "Oct",
    "Nov",
    "Dec",
  ];
  return months[month - 1];
}
</script>



<style scoped>
#search-box {
  width: 400px;
  margin: 20px;
  padding: 20px;
  opacity: 0.9;
  height: 40px !important;
}
.search-btn {
  margin: 20px 0 20px 10px;
  height: 40px !important;
  border: #ff5252;
  background-color: #ff5252;
}
.search-btn:hover {
  background-color: #fa6d6d;
  border: #ff5252 !important;
}
.search-btn:active {
  background-color: #fa6d6d !important;
  border: #ff5252 !important;
}
.search-btn:focus {
  background-color: #fa6d6d !important;
  border: #ff5252 !important;
}
.heading {
  color: rgb(216, 89, 115);
  padding-top: 70px;
}
.current {
  color: white;
  border-color: white;
  border: solid #000;
  border-width: 0 1px;
  opacity: 0.7;
  border: darkred;
}
.weather-degree {
  width: 100%;
  height: min-content;
}
.degree {
  margin: 30px;
  vertical-align: bottom;
  font-size: 1.4rem;
  display: flex;
  color: aliceblue;
  opacity: 0.7;
}
</style>