<template>
  <InputUser @form-submitted="updateFormData" />
  <SearchData :formData="formData" />
</template>

<script>
import InputUser from './components/InputUser.vue'
import SearchData from './components/SearchData.vue';

export default {
  name: 'App',
  components: {
    InputUser,
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
body {
  background-color: #323650;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin: 0px;
  height: 100vh;
  width: 100%;
  display: flex;
  align-items: center;
  flex-direction: column;
  -webkit-animation: fadeIn 2s ease-in-out;
  -moz-animation: fadeIn 2s ease-in-out;
  -o-animation: fadeIn 2s ease-in-out;
  animation: fadeIn 2s ease-in-out;
}

@-webkit-keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
@-moz-keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
@-o-keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
</style>
