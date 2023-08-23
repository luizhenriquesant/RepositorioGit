<template>
  <div>
    <input v-model="nameData" placeholder="Nome">
    <button @click="submitForm">Enviar</button>
  </div>
</template>

<script>
export default {
  name: 'InputUser',
  data() {
    return {
      nameData: '',
    }
  }, methods: {
    submitForm() {
      this.$emit('form-submitted', { nameData: this.nameData });
    },
  },
}
</script>

<style scoped>
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
