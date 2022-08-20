<template>
<div class="d-flex main-wrap">
  <div>
    <StatSheet></StatSheet>
  </div>
</div>
</template>

<script>
import StatSheet from "./views/StatSheet"

export default {
  name: 'App',
  components: {
    StatSheet
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.main-wrap {
  flex-wrap: wrap;
}
</style>
