<template>
    <div class="searchInput">
      <input class="inputField" v-model="inputUrl" placeholder=" Copiez un lien Sf-Clothe or Shopify ici " />
      <button class="searchButton" @click="fetchData">Trouvez votre vetêment</button>
  
      <div v-if="Object.keys(responseData).length !== 0">
        <h3>Vêtement correspondant :</h3>
        <div :style="{backgroundColor: cardBackgroundColor}"  class="card" ref="card">
          <img class="" :src="responseData.imageUrl" alt="Product Image" />
          <div class="card-content">
            
            <p>Nom : {{ responseData.name ? responseData.name : 'N/A' }}</p>
            <p>Taille : {{ responseData.size ? responseData.size.label : 'N/A' }}</p>
            
            <p>Prix : {{ responseData.price }}€</p>
          </div>
        </div>
        <div class="card-actions">
          <div class="color-picker">
            <h4>Choisir une couleur :</h4>
            <ul class="color-list">
              <li v-for="color in colorList" :key="color" :style="{ backgroundColor: color }" @click="selectColor(color)"></li>
            </ul>
          </div>
          <button @click="extractPhoto">Extraire la photo</button>
        </div>
      </div>
    </div>
</template>
  

<script>
import html2canvas from 'html2canvas';
export default {
    data() {
        return {
            inputUrl: '',
            showModal: false,
            responseData: {},
            cardBackgroundColor: '#fff',
            colorList: ['#f28b82', '#fbbc04', '#fff475', '#ccff90', '#a7ffeb', '#cbf0f8', '#aecbfa', '#d7aefb', '#fdcfe8', '#e6c9a8', '#e8eaed']
        }
    },
  name: 'HomeComponent',
  props: {
    titleInput: String
  },
  methods: {
    selectColor(color) {
      this.cardBackgroundColor = color;
    },
    fetchData() {
      fetch(this.inputUrl)
        .then(response => response.json())
        .then(data => {
            this.responseData = data;
          console.log('Données reçues :', data);
        })
        .catch(error => {
          console.error('Une erreur s\'est produite lors de la requête API :', error);
        });
    },
    extractPhoto() {
      const cardElement = this.$refs.card;

    html2canvas(cardElement).then((canvas) => {
      const image = canvas.toDataURL('image/png');

      const link = document.createElement('a');
      link.href = image;
      link.download = 'extracted_photo.png';
      link.click();
    });
    },
  },
}
</script>

<style scoped>

.color-picker {
  margin-top: 20px;
}

.color-list {
  display: flex;
  list-style: none;
  padding: 0;
}

.color-list li {
  width: 30px;
  height: 30px;
  margin-right: 10px;
  cursor: pointer;
  border: 1px solid #ccc;
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

.searchInput{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border-radius: 10rem;
}

.inputField{
    width: 50%;
    padding: 12px 20px;
    margin: 8px 0;
    box-sizing: border-box;
    border-radius: 1rem;
}

.searchButton{
    background-color: #4CAF50;
    border: none;
    border-radius: 10rem;
    color: white;
    padding: 16px 32px;
    text-decoration: none;
    margin: 4px 2px;
    cursor: pointer;
}

.card {
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 16px;
  margin-bottom: 16px;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.card img {
  width: 200px;
  height: 200px;
  object-fit: cover;
  border-radius: 10px;
  margin-bottom: 16px;
}

.card-content {
  margin-top: 16px;
}

.card p {
  margin-bottom: 8px;
}
</style>