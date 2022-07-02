<template>
  <div class="home">
    <Earth />
  </div>
</template>

<script>
// @ is an alias to /src
import Earth from "@/components/SliderEarth.vue";

export default {
  name: "Home",
  components: {
    Earth,
  },
};
</script>
