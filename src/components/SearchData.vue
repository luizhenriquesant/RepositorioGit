<template>
    <header>
        <img circle size="sm" :src="user.avatar_url" />
        <h3>Name</h3>
        <span>{{ user.name }}</span>
        <hr />
        <h3>Git Profile</h3>
        <span><a :href="user.html_url" target="_blank">{{ user.login }}</a></span>
        <hr />
        <h3>Repository</h3>
        <br>
        
        <div class="repositorios">
            <ul id="myList" v-if="repos.length > 0">       
                <input type="text" v-model="search" placeholder="search repository" /><br>   
                <small>Total: {{ repos.length }}</small>
                <li v-for="repository in filteredRepos" :key="repository.id">
                    <a :href="repository.html_url" target="_blank">{{ repository.name }}</a>
                </li>
            </ul>
        </div>
    </header>
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

input {
  border: 0;
  border-bottom: 2px solid #9e9e9e;
  outline: none;
  transition: 0.2s ease-in-out;
  box-sizing: border-box;
}

img {
  border-radius: 50%;
}
.sm {
  height: 80px;
  float: left;
  padding: 0 10px;
}

header {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background: #fff;
    flex-wrap: wrap;
    width: 80%;
    margin-top: 20px;
}

hr {
    width: 100%;
    margin-bottom: 10px;
}

h3 {
    margin: 5px 0 0 0;
}

a{
    font-weight: 500;
    font-family: "Courier New", Courier, monospace;
    font-size: 16px;
    text-align: center;
    margin-top: 5px;
}

span {
    font-weight: 500;
    font-family: "Courier New", Courier, monospace;
    font-size: 16px;
    text-align: center;
    margin-top: 5px;
}

.link {
    text-decoration: none;
    color: #000;
    font-weight: 500;
    font-family: "Courier New", Courier, monospace;
    font-size: 16px;
    text-align: center;
}

.link:hover {
    color: blue;
}

.repositorios {
  display: flex;
  justify-content: flex-start;
  align-self: flex-start;
  flex-direction: column;
  width: 92%;
}

.repositorios h4 {
  text-align: center;
}

.card {
  max-width: 70ch;
  margin-top: 40px;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: #fff;
  flex-wrap: wrap;
  border-radius: 5px;
  background-size: cover;
  background-position: center center;
  box-shadow: 30px 30px 30px -5px rgba(0, 0, 0, 0.3);
  transition: box-shadow 0.5s;
  will-change: transform;
  border: 15px solid white;
  margin-bottom: 40px;
}

.card:hover {
  box-shadow: 30px 30px 30px 35px rgba(0, 0, 0, 0.3);
}

ul > h4 {
  margin-bottom: 2px;
}

#listRepos {
  position: absolute;
  width: 80vw;
}
#listRepos li {
  visibility: hidden;
  -webkit-animation: fadeIn 2s ease-in-out;
  -moz-animation: fadeIn 2s ease-in-out;
  -o-animation: fadeIn 2s ease-in-out;
  animation: fadeIn 2s ease-in-out;
}
#listRepos li:nth-child(2n) {
  background-color: #444;
  color: #2de;
  padding: 6px 0;
  list-style: none;
}

#listRepos li:nth-child(2n + 1) {
  background-color: #333;
  color: white;
  padding: 6px 0;
  list-style: none;
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
