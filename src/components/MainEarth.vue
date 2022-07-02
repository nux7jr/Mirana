<template>
  <div class="main">
    <h1>Earth</h1>
    <div class="Earth" v-if="isLoading === false">
      <div v-for="(item, index) in planetData" v-bind:key="item.id">
        <div class="earth__wrapper" v-show="index == hoursValue">
          <img
            class="main__media"
            :src="`https://epic.gsfc.nasa.gov/archive/natural/${userFormDate.userYear}/${userFormDate.userMonth}/${userFormDate.userDay}/jpg/${item.image}.jpg`"
            alt="img"
          />
        </div>
      </div>
    </div>
    <div v-else>
      <h1>Loading</h1>
    </div>
    <div class="option">
      <div class="slidecontainer">
        <input
          class="option__range"
          type="range"
          min="0"
          :max="planetData.length - 1"
          range="1"
          value="0"
          v-model.number="hoursValue"
        />
      </div>
      <div>
        <form @submit.prevent="getData">
          <div class="form__item">
            <label class="form__label" for="year">Year</label>
            <input
              class="form__input"
              type="text"
              id="year"
              v-model="modalFormDate.userYear"
              required
            />
          </div>
          <div class="form__item">
            <label class="form__label" for="month">Month</label>
            <input
              class="form__input"
              id="month"
              type="text"
              v-model="modalFormDate.userMonth"
              required
            />
          </div>
          <div class="form__item">
            <label class="form__label" for="day">Day</label>
            <input
              class="form__input"
              type="text"
              id="day"
              v-model="modalFormDate.userDay"
              required
            />
          </div>
          <button class="form__btn">Send</button>
        </form>
      </div>
    </div>
    <!-- {{ hoursValue }}
    {{ userFormDate.userYear }}
    {{ userFormDate.userMonth }}
    {{ userFormDate.userDay }} -->
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "Earth",
  data() {
    return {
      modalFormDate: {
        userYear: "2020",
        userMonth: "10",
        userDay: "31",
      },
      userFormDate: {
        userYear: "2020",
        userMonth: "10",
        userDay: "31",
      },
      isLoading: true,
      hoursValue: 0,
      planetData: [],
      // currUrl: "https://api.nasa.gov/EPIC/api/natural/date/",
      apiKey: "n4vyXT7xMphVZN3IZIUaQW7pBJvSAAeuxhz9HZsI",
    };
  },
  created() {
    this.getData();
  },
  methods: {
    async getData() {
      this.userFormDate.userYear = this.modalFormDate.userYear;
      this.userFormDate.userYear = this.modalFormDate.userYear;
      this.userFormDate.userDay = this.modalFormDate.userDay;
      const res = await axios.get(
        `https://api.nasa.gov/EPIC/api/natural/date/${this.userFormDate.userYear}-${this.userFormDate.userMonth}-${this.userFormDate.userDay}` +
          "?api_key=" +
          this.apiKey
      );
      this.isLoading = false;
      this.planetData = res.data;
      this.hoursValue = 0;
      // try {
      //   const res = await axios.get(
      //     `https://api.nasa.gov/EPIC/api/natural/date/${this.userFormDate.userYear}-${this.userFormDate.userMonth}-${this.userFormDate.userDay}` +
      //       "?api_key=" +
      //       this.apiKey
      //   );
      //   this.isLoading = false;
      //   this.planetData = res.data;
      //   this.hoursValue = 0;
      // } catch (err) {
      //   console.error(err);
      // }
    },
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
  margin: 0 auto;
}
img {
  border-radius: 100%;
  max-width: 780px;
  max-height: 780px;
  box-shadow: 0 0 0 3px rgb(0, 0, 0), 0 0 13px #333;
}
.option__range {
  width: 150px;
  margin-top: 20px;
}
.earth__wrapper {
  margin: 0 auto;
  background-color: black;
  border-radius: 100%;
  max-width: 780px;
  max-height: 780px;
}
.form__input {
  width: 50px;
  font-size: 13px;
  padding: 6px 0 4px 10px;
  border: 1px solid #cecece;
  background: #f6f6f66b;
  border-radius: 8px;
  color: #f6f6f6;
}
.form__label {
  margin: 20px;
  text-align: left;
}
.form__item {
  margin: 10px 0;
}
.form__btn {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-weight: 600;
  font-size: 16px;
  padding: 10px;
  margin-bottom: 30px;
  border: 1px solid #cecece;
  background: #f6f6f66b;
  color: white;
  border-radius: 8px;
}
</style>
