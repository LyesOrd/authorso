<template>
    <div class="searchInput">
      <input class="inputField" v-model="inputUrl" placeholder=" Copiez un lien Sf-Clothe or Shopify ici " />
      <button class="searchButton" @click="apiRequestMethod">Trouvez votre vetêment</button>
  
      <div v-if="Object.keys(responseData).length !== 0">
        <h3>Vêtement correspondant :</h3>
        <div :style="{backgroundImage: cardBackgroundColor}"  class="card card_container" ref="card" @mousedown="startResize">
          <img class="" :src="responseData.imageUrl" alt="Image du vêtement" />
          <div class="card-content">
            
            <p>Nom : {{ responseData.name ? responseData.name : 'Aucun' }}</p>
            <p>Taille : {{ responseData.size ? responseData.size.label : 'Aucun' }}</p>
            
            <p>Prix : {{ responseData.price }}€</p>
          </div>
        </div>
      </div>
      <div v-if="Object.keys(responseData).length !== 0" class="card-actions">
          <div class="color-picker">
            <h4>Choisir une couleur :</h4>
            <ul class="color-list">
              <li class="colorButton" v-for="color in colorList" :key="color" :style="{ backgroundImage: color }" @click="selectColor(color)"></li>
            </ul>
          </div>
          <button class="searchButton" @click="extractPhoto"><i class="fa fa-download"></i> Extraire la photo</button>
          <button class="facebookButton" @click="shareOnFacebook"><i class="fab fa-facebook"></i> Partager sur Facebook</button>
          <button class="instagramButton" @click="shareOnInstagram"><i class="fab fa-instagram"></i> Partager sur Instagram</button>

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
            colorList: [
              'linear-gradient(to right, #ff4081, #9c27b0)',    
              'linear-gradient(to right, #ff5722, #ff9800)',    
              'linear-gradient(to right, #f44336, #e91e63)',    
              'linear-gradient(to right, #e91e63, #9c27b0)',    
              'linear-gradient(to right, #3f51b5, #2196f3)',    
              'linear-gradient(to right, #4caf50, #8bc34a)',
              'linear-gradient(to right, #ffcc00, #ff3300)',
              'linear-gradient(to right, #00ff00, #00ccff)',   
              'linear-gradient(to right, #ff0099, #6600cc)',   
              'linear-gradient(to right, #ff99cc, #33ccff)',   
              'linear-gradient(to right, #ffff00, #ff00ff)'    
            ],
            cardBackgroundColor: 'linear-gradient(to right, #4286f4, #00cc99)',
            cardWidth: 400,
        }
    },
  name: 'HomeComponent',
  props: {
    titleInput: String
  },
  methods: {

    startResize(event){
      event.preventDefault();

      const initialWidth = this.$refs.card.offsetWidth;
      window.addEventListener('mousemove', this.resize);
      window.addEventListener('mouseup', this.stopResize);

      this.resizeData = {
        initialWidth,
        x: event.clientX,
      };
    },

    resize(event){
      const cardElement = this.$refs.card;
      const { initialWidth, x } = this.resizeData;
      const newWidth = initialWidth + (event.clientX - x);

      cardElement.style.width = `${newWidth}px`;
    },

    stopResize(){
      window.removeEventListener('mousemove', this.resize);
      window.removeEventListener('mouseup', this.stopResize);

      this.resizeData = null;
    },

    selectColor(color) {
      this.cardBackgroundColor = color;
    },
    apiRequestMethod() {
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

      html2canvas(cardElement, {
        backgroundColor: null,
        scale: 2,
        useCORS: true,
      }).then((canvas) => {
        const image = canvas.toDataURL('image/png');

        const link = document.createElement('a');
        link.href = image;
        link.download = `${this.responseData.name}.png`
        link.click();
      });
    },
    shareOnFacebook() {
      const shareUrl = `https://www.facebook.com/sharer/sharer.php?u=${this.inputUrl}`;
      window.open(shareUrl, '_blank');
    },
    shareOnInstagram() {
      const shareUrl = `https://www.instagram.com/?url=${this.inputUrl}`;
      window.open(shareUrl, '_blank');
    }
  }
}
</script>

<style scoped>

.card-container {
  position: relative;
  background: inherit;
}

.card-container::before, .card-container::after {
  content: '';
  position: absolute;
  width: 10px;
  height: 10px;
  background: #000;
  cursor: nwse-resize;
}

.card-container::after {
  right: -5px;
  bottom: -5px;
}

.card-container::before {
  top: -5px;
  left: -5px;
}

.facebookButton{
    background-color: #3b5998;
    border: none;
    border-radius: 10rem;
    color: white;
    padding: 16px 32px;
    text-decoration: none;
    margin: 4px 2px;
    cursor: pointer;
}

.instagramButton{
    background-color: #C13584;
    border: none;
    border-radius: 10rem;
    color: white;
    padding: 16px 32px;
    text-decoration: none;
    margin: 4px 2px;
    cursor: pointer;
}

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
  border-radius: 50%;
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
  min-width: 400px;
  max-width: 1080px;
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