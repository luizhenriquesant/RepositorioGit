<template>
  <HelloWorld @form-submitted="updateFormData" />
  <SearchData :formData="formData" />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import SearchData from './components/SearchData.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
    SearchData,
  },
  data() {
    return {
      formData: {},
    };
  },
  methods: {
    updateFormData(data) {
      this.formData = data;
    },
  },
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
</style>
