<template>
  <div class="about">
    <h1>About Botaminder</h1>
    <p>Botaminder is a Arduino Project by Team FreshBOTS to build a simple to use desk clock with a lot of customisation and functionality in mind. </p>
  </div>
  <div class="dependencies">
    <h3>Made with</h3>
    <w-tag class = "ma1" bg-color = "success" color='white' xl>VueJS</w-tag>
    <w-tag class = "ma1" bg-color = "light blue" color='white' xl>Wave UI</w-tag>
  </div>
  <Footer></Footer>
</template>


<script>
import Footer from '@/components/Footer.vue'
export default {
  name: 'About',
  components: {
    Footer,
  }
}
</script>

<style scoped>
* {
  padding-top: 10px;
}
</style>