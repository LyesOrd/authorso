<template>
    <div class="searchInput">
      <input class="inputField" v-model="inputUrl" placeholder="Entrez l'URL" />
      <button class="searchButton" @click="fetchData">Obtenir les informations</button>
  
      <v-dialog v-model="showModal" width="800">
        <template v-slot:activator="{ props }">
          <v-btn v-if="responseData" color="primary" v-bind="props">
            Liste des vetements
          </v-btn>
        </template>
        <v-card>
          <v-card-title>
            <span class="text-h5">Liste des vêtements</span>
          </v-card-title>
          <v-card-text>
            <v-list>
              <v-list-item v-for="(item, index) in responseData" :key="index">
                {{ item }}
                <v-list-item-content>
                  <v-list-item-title>{{ item.name }}</v-list-item-title>
                  <v-list-item-subtitle>{{ item.amount }}</v-list-item-subtitle>
                </v-list-item-content>
              </v-list-item>
            </v-list>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn v-if="responseData" color="#173f4e" variant="text" @click="showModal = false">
              Fermer
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </div>
</template>
  

<script>
export default {
    data() {
        return {
            inputUrl: '',
            showModal: false,
            responseData: [],
        }
    },
  name: 'HomeComponent',
  props: {
    titleInput: String
  },
  methods: {
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
  },
}
</script>

<style scoped>
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
}

.inputField{
    width: 50%;
    padding: 12px 20px;
    margin: 8px 0;
    box-sizing: border-box;
}

.searchButton{
    background-color: #4CAF50;
    border: none;
    color: white;
    padding: 16px 32px;
    text-decoration: none;
    margin: 4px 2px;
    cursor: pointer;
}
</style>