<template>
  <div>
    <div class="col-xs-12 col-sm-12 text-center contain">
      <div>
        <h4>Other Information</h4>
      </div>
      <div class="details">
        <div class="title">High/Low</div>
        <div class="info">{{high}}</div>
      </div>
      <div class="details">
        <div class="title">Wind</div>
        <div class="info">{{wind}}</div>
      </div>
      <div class="details">
        <div class="title">Humidity</div>
        <div class="info">{{humidity}}</div>
      </div>
      <div class="details">
        <div class="title">Visiblity</div>
        <div class="info">{{info}}</div>
      </div>
    </div>
  </div>
</template>

<script>
import {eventBus} from '../main'
export default {
  data() {
    return {
      high: "____",
      wind: "____",
      humidity: "____",
      info: "____",
    };
  },
  created() {
    console.log("created");
    eventBus.$on("newData", (data) => {
      this.high=data.high;
      this.wind=data.wind;
      this.humidity=data.humidity;
      this.info=data.info;
      console.log(data);
    });
  },
};
</script>

<style scoped>
.text-center {
  padding-top: 40px;
}

.contain {
  text-align: center;
  margin: auto;
  width: 500px;
  height: 400px;
  position: relative;
}

h4 {
  color: white;
  opacity: 0.7;
}

.title {
  float: left;
  color: white;
  opacity: 0.9;
  font-size: 1.2rem;
  padding-left: 40px;
}

.details {
  padding: 20px;
}
.info {
  float: right;
  color: white;

  font-size: 1.2rem;
  opacity: 0.7;
  padding-right: 40px;
}
@media only screen and (max-width: 500px) {
  /* For mobile phones: */
  .contain {
    width: 100%;
  }
}
</style>