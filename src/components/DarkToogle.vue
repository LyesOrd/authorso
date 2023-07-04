<template>
    <button @click="toggleDarkMode">
        {{ darkMode }}
        Basculer en mode {{ darkMode !== 'dark' ? 'clair' : 'sombre' }}
    </button>
  </template>
  
  <script>
  export default {
    methods: {
      toggleDarkMode() {
        this.$emit('toggle-dark-mode'); // Émet un événement pour basculer le mode sombre dans le composant parent
      },
    },
  };
  </script>
  
  <style scoped>
  button {
    background-color: #42b983;
    border: none;
    border-radius: 4px;
    color: #fff;
    cursor: pointer;
    font-size: 14px;
    font-weight: 600;
    padding: 10px 15px;
  }
  </style>
  