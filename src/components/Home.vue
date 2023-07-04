<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h4>
      Copipez l'url d'un vêtement de la boutique en ligne sf-clothes pour avoir les informations de ce vêtement
    </h4>
  </div>
</template>

<script>
export default {
  name: 'HomeComponent',
  props: {
    msg: String
  }
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
