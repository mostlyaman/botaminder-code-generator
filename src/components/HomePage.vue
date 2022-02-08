<template>
  <h1>Botaminder</h1>
  <h2>Arduino Script Generator</h2>
  <div class="container">
    <w-button @click = "this.$router.push('/manual')" class="ma1" bg-color="secondary" lg>Add Events Manually</w-button>
    <w-button class="ma1" bg-color="secondary" lg>Import Events from Google Calendar</w-button>
  </div>
</template>

<script>
export default {
  name: 'HomePage',
  props: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.container{
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 100px;
  border: 2px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
