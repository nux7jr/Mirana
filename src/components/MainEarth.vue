<template>
  <div class="main">
    <h1>Earth</h1>
    <div class="Earth" v-if="isLoading === false">
      <div v-for="(item, index) in planetData" v-bind:key="item.id">
        <div class="earth__img" v-show="index == hoursValue">
          <img
            class="main__media"
            :src="
              index == hoursValue
                ? `https://epic.gsfc.nasa.gov/archive/natural/${userFormDate.userYear}/${userFormDate.userMonth}/${userFormDate.userDay}/jpg/${item.image}.jpg`
                : null
            "
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
          class="setDate"
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
            <label class="form__label" for="year">Год</label>
            <input
              class="form__input"
              type="text"
              id="year"
              v-model="userFormDate.userYear"
              required
            />
          </div>
          <div class="form__item">
            <label class="form__label" for="month">Месяц</label>
            <input
              class="form__input"
              id="month"
              type="text"
              v-model="userFormDate.userMonth"
              required
            />
          </div>
          <div class="form__item">
            <label class="form__label" for="day">Число</label>
            <input
              class="form__input"
              type="text"
              id="day"
              v-model="userFormDate.userDay"
              required
            />
          </div>
          <button class="form__btn">Отправить</button>
        </form>
      </div>
    </div>
    {{ hoursValue }}
    {{ userFormDate.userYear }}
    {{ userFormDate.userMonth }}
    {{ userFormDate.userDay }}
  </div>
</template>
<script>
import axios from "axios";

export default {
  name: "Earth",
  data() {
    return {
      userFormDate: {
        userYear: "2020",
        userMonth: "10",
        userDay: "31",
      },
      isLoading: true,
      hoursValue: 0,
      planetData: [],
      currUrl: "https://api.nasa.gov/EPIC/api/natural/date/2020-10-31",
      apiKey: "n4vyXT7xMphVZN3IZIUaQW7pBJvSAAeuxhz9HZsI",
    };
  },
  created() {
    this.getData();
  },
  methods: {
    async getData() {
      const res = await axios.get(
        `https://api.nasa.gov/EPIC/api/natural/date/${this.userFormDate.userYear}-${this.userFormDate.userMonth}-${this.userFormDate.userDay}` +
          "?api_key=" +
          this.apiKey
      );
      this.isLoading = false;
      this.planetData = res.data;
      this.hoursValue = 0;
      console.log(this.planetData);
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
  box-shadow: 0 0 0 3px rgb(0, 0, 0), 0 0 13px #333;
}
.setDate {
  width: 150px;
}
.earth__img {
  background-color: black;
  border-radius: 50%;
  height: 954px;
}
img {
  width: 100%;
  height: 100%;
}
</style>
