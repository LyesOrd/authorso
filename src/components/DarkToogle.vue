<template>
    <button @click="toggleDarkMode">
        <i v-if="darkMode" class="fas fa-sun"></i>
        <i v-else class="fas fa-moon"></i>
    </button>
  </template>
  
  <script>
  export default {
    props: {
      darkMode: Boolean,
    },
    computed: {
      darkButton() {
        return this.$parent.darkMode ? 'Mode sombre' : 'Mode sombre';
      },
    },
    methods: {
      toggleDarkMode() {
        this.$emit('toggle-dark-mode'); // Émet un événement pour basculer le mode sombre dans le composant parent
      },
    },
  };
  </script>
  
  <style scoped>
  button {
    border: none;
    border-radius: 10rem;
    cursor: pointer;
    font-size: 25px;
    font-weight: 600;
    padding: 10px 15px;
  }
  </style>
  