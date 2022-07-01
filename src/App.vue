<template>
  <div id="app" class="gradient">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;
  min-height: 100vh;
}
.gradient {
  width: 100%;
  background: linear-gradient(
    149deg,
    rgba(24, 187, 156, 1) 0%,
    rgba(106, 57, 175, 1) 42%,
    rgba(187, 24, 148, 1) 72%,
    rgba(115, 53, 134, 1) 100%
  );
  animation: gradient 10s infinite linear;
  background-size: 400%;
}

@keyframes gradient {
  0% {
    background-position: 80% 0%;
  }
  50% {
    background-position: 20% 100%;
  }
  100% {
    background-position: 80% 0%;
  }
}
body {
  padding: 0;
  margin: 0;
}
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  border: 0;
  clip: rect(0 0 0 0);
}
ul,
li {
  margin: 0;
  padding: 0;
  list-style: none;
}
a {
  text-decoration: none;
}
img {
  width: 100%;
  height: auto;
}
#nav {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
  padding: 30px;

  a {
    font-weight: bold;
    color: #ffffff;

    &.router-link-exact-active {
      color: #d4dbd8;
    }
  }
}
</style>
