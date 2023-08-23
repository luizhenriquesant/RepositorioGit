<template>
    <div class="user">
        <div class="image">
            <img :src="user.avatar_url" />
        </div>
        <div class="name">
            {{ user.login }}
        </div>

    </div>
    <input type="text" v-model="search" placeholder="search repository" />
    <div class="repositorios">
        <ul id="myList" v-if="repos.length > 0">
            <h4>Repositórios</h4>
            <small>Total: {{ repos.length }}</small>
            <li v-for="repository in filteredRepos" :key="repository.id">
                <a :href="repository.html_url" target="_blank">{{ repository.name }}</a>
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
            repos: {},
            search: ""
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
    computed: {
        filteredRepos: function () {
            return this.repos.filter((repository) => {
                return repository.name.match(this.search);
            });
        }
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
<style scoped>
</style>
