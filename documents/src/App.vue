<template>
  <nav>
    <router-link class="router" to="/"> Projects </router-link> |
    <router-link class="router" to="/add"> Add New Project </router-link>
    <label for=""  id="dark-change" @click="darkMode" ></label>
  </nav>
  <br>
  <BackandGo :style="forBackandGo" />
  <router-view/>
</template>

<script>

import BackandGo from './components/BackandGo.vue';
  export default {
    components: {
      BackandGo
    },
    data () {
      return {
        forBackandGo: "background: white; padding: 5px; border-radius: 5px;"
      }
    },
    methods: {
      darkMode () {
        const content = document.getElementsByTagName('body')[0];
        const darkMode = document.getElementById('dark-change');
        darkMode.addEventListener('click', function () {
        darkMode.classList.toggle('active');
        content.classList.toggle('night');
      })
      }
    },
  }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 600px;
  margin: 0 auto;
  text-decoration: none;
  
}

nav {
  text-align: center;
}


.router {
  text-decoration: none;
  color: black;
  font-size: larger;
  background: white;
  padding: 5px;
  border-radius: 5px;
}

.colorWhite {
  color: white;
}

.router:hover {
  font-weight: bold;
  border-bottom: 3px solid #20639B;
}

.router-link-active {
  color: #20639B;
  font-weight: bolder;
}

label {
  
  position: fixed;
  width: 45px;
  height: 22px;
  right: 20px;
  top: 20px;
  border: 2px solid;
  border-radius: 20px;
}

label:before{
  position: absolute;
  content: '';
  width:20px;
  height: 20px;
  left: 1px;
  top: 1px;
  border-radius: 50%;
  background: #000;
  cursor: pointer;
  transition: 0.4s;
}

label.active:before{
  left: 24px;
  background: #fff;
}

body.night{
  background: #292C35;
  color: white;
}

</style>
