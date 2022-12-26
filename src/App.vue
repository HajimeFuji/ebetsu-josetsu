<template>

<main>
  <router-view/>
</main>

</template>

<script>
import 'normalize.css'

export default {
  name: 'App',
}
</script>

<style lang="scss">

html {
  width: 100%;
  height: 100%;
  overflow-x: hidden;
}

body {
  width: 100%;
  height: 100%;
}

main {
    height: 100%;
}

#app {
  font-family: Avenir, Helvetica, Arial, Hiragino sans, sans-serif, Noto Sans CJK JP;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 100vw;
  height: 100%;
}
</style>
