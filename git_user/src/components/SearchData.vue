<template>
    <div class="user">
        <div>User Component</div>
        <div class="image">
            <img :src="user.avatar_url" />
        </div>
        <div class="name">
            {{ user.login }}
        </div>
        
    </div>
    <div class="repositorios">
        <ul id="myList" v-if="repos.length > 0">
          <h4>Repositórios</h4>
          <small>Total: {{ repos.length }}</small>
          <hr />
          <li v-for="repository in repos" :key="repository.id">
            {{ repository.name }}
          </li>
        </ul>
      </div>
</template>
  
<script>
import axios from "axios";

export default {
    name: "SearchData",
    props: ['formData'],
    data() {
        return {
            user: {},
            repos: {}
        };
    },
    watch: {
        formData: {
            immediate: true,
            handler(newValue) {
                this.getUser(newValue.nameData);
                this.getRepos(newValue.nameData);
            },
        },
    },
    methods: {
        getUser() {
            
            axios
                .get(`https://api.github.com/users/${this.formData.nameData}`)
                .then((res) => {
                    this.user = res.data;
                })
                .catch((error) => {
                    console.log(error);
                });
        },
        getRepos() {
            axios
                .get(`https://api.github.com/users/${this.formData.nameData}/repos`)
                .then((res) => {
                    this.repos = res.data;
                })
                .catch((error) => {
                    console.log(error);
                });
        },

    },
};
</script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
  