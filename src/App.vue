<template>
  <div id="app">
    <b-container class="bv-example-row">
      <b-row>
          <b-col cols="7"> <Form msg="Welcome to Your Vue.js App"/></b-col>
          <b-col cols="5"></b-col>
      </b-row>
  </b-container>

  </div>
</template>

<script>
import Form from './components/Form.vue'


export default {
  name: 'app',
  components: {
    Form
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
