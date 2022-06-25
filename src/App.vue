<template>
  <div id="app">
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
  color: #dedfe0;
  background: rgb(86, 81, 164);
  background: linear-gradient(
    90deg,
    rgba(86, 81, 164, 1) 0%,
    rgba(0, 0, 0, 1) 5%,
    rgba(0, 0, 0, 1) 48%,
    rgba(0, 0, 0, 1) 96%,
    rgba(141, 111, 204, 1) 100%
  );
  min-height: 100vh;
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
  padding: 30px;

  a {
    font-weight: bold;
    color: #d6dde4;

    &.router-link-exact-active {
      color: #757977;
    }
  }
}
</style>
