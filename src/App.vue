<template>
  <div :class="{dark: darkMode}">
    <div class="header">
      <img id="logoPage" alt="Vue logo" src="./assets/online_shopping.jpg">
      <DarkToogle :darkMode="darkMode" @toggle-dark-mode="toggleDarkMode" />
    </div>
    
    <Home msg="Clothes.so"/>
    <SearchClothes msg="Chercher votre vêtement"/>
  </div>
</template>

<script>
import Home from './components/Home.vue'
import SearchClothes from './components/SearchClothes.vue'
import DarkToogle from './components/DarkToogle.vue'

export default {
  data() {
    return {
      darkMode: false,
    }
  },
  name: 'App',
  components: {
    Home,
    SearchClothes,
    DarkToogle,
  },
  methods: {
    toggleDarkMode() {
      this.darkMode = !this.darkMode;
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
}

#logoPage{
  width: 100px;
  height: 100px;
  border-radius: 50%;
}
.dark {
  background-color: #2c3e50;
  color: #fff;
}

.header{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  margin: 0;
  padding: 0;

}
</style>
