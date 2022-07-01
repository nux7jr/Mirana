<template>
  <div class="main">
    <h1>Earth</h1>
    <div v-for="(item, index) in data" v-bind:key="item.id">
      <div v-show="index == valueDate">
        <img
          class="main__media"
          :src="`https://epic.gsfc.nasa.gov/archive/natural/2020/10/31/jpg/${item.image}.jpg`"
          alt="img"
        />
      </div>
    </div>
    <div class="slidecontainer">
      <input
        class="setDate"
        type="range"
        min="0"
        max="11"
        range="1"
        value="0"
        v-model.number="valueDate"
      />
    </div>
    <div>
      <form @submit.prevent="sendData">
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
      valueDate: 0,
      inputDate: "",
      formDateUrl: "",
      data: [],
      currUrl: "https://api.nasa.gov/EPIC/api/natural/date/2020-10-31",
      apiKey: "n4vyXT7xMphVZN3IZIUaQW7pBJvSAAeuxhz9HZsI",
    };
  },
  async created() {
    const res = await axios.get(this.currUrl + "?api_key=" + this.apiKey);
    this.data = res.data;
    console.log(this.data);
    this.myTrue = true;
  },
  methods: {
    getData() {
      console.log("getData");
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
  max-width: 40%;
  max-height: 40%;
  margin: 0 auto;
}
img {
  margin: 0 auto;
  border-radius: 100%;
  box-shadow: 0 0 0 3px rgb(0, 0, 0), 0 0 13px #333;
}
.setDate {
  width: 150px;
}
</style>
