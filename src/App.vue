<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style lang="scss">
#app {
  perspective: 100vmin;
  overflow: hidden;
  background: lightblue;
  height: 100vh;
  width: 100vw;
  box-sizing: border-box;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
