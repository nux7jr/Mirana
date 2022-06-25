<template>
  <div class="main">
    <h1>Earth</h1>
    <div class="main__media">
      <!-- <img
        class="main__img"
        src="https://api.nasa.gov/EPIC/archive/natural/2019/05/30/png/epic_1b_20190530011359.png?api_key=n4vyXT7xMphVZN3IZIUaQW7pBJvSAAeuxhz9HZsI"
        alt=""
      /> -->
    </div>
    <div v-for="item in data" :key="item.id">
      <div><h2>elem</h2></div>
      date: {{ item.date }} name: {{ item.image }}
      <img src="" alt="" />
    </div>
    <div class="slidecontainer">
      <input
        class="setDate"
        type="range"
        min="1"
        max="12"
        range="1"
        value="1"
        v-model.number="valueDate"
      />
    </div>
    <div>{{ valueDate }}</div>
    <div><button>setUrl</button> <button>setUrl</button></div>
    <div>{{ currUrl }}</div>
    <input type="date" name="date" id="" v-model="inputDate" />
    <div>{{ inputDate }}</div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  name: "Earth",
  data() {
    return {
      valueDate: 1,
      inputDate: "",
      defaultMaxRange: 12,
      data: [],
      currUrl: "https://api.nasa.gov/EPIC/api/natural/date/2021-10-31",
      apiKey: "n4vyXT7xMphVZN3IZIUaQW7pBJvSAAeuxhz9HZsI",
    };
  },
  async created() {
    const res = await axios.get(this.currUrl + "?api_key=" + this.apiKey);
    this.data = res.data;
    console.log(this.data);
    this.defaultMaxRange = this.data.length;
    console.log(this.defaultMaxRange);
  },
};
</script>
<style scoped>
.main {
  color: white;
  width: 100%;
}
.main__media {
  display: block;
  width: 70%;
  height: 70%;
  margin: 0 auto;
}
img {
  margin: 0 auto;
}
.setDate {
  width: 60%;
}
</style>
