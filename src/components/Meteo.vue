<template>
  <div class="container">
    <h1 class="my-4">App Meteo Vue.js</h1>
    <div class="form-groupe mb-5">
      <label for="position">Entrez le nom d'une ville</label>
      <input id="position" 
             type="text"
             class="form-control"
             v-model="requete"
             @keypress.enter="goMeteo">
    </div>

    <div v-if="temps" class="w-75 m-auto">
      <h3 class="text-center mb-4">Position : {{ temps.name }}</h3>
      <div class="card text-center p-5">
        <p class="texte-affichage">Température : {{ temps.main.temp.toFixed(1) }} °</p>
        <p class="texte-affichage">Temps : {{ temps.weather[0].description }} </p>
      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios'

  export default {
    name: 'Meteo',
    data(){
      return{
        requete: '',
        temps: undefined,
        apiCode: 'd79aff907bf0057b84022135f6dc0f10',
        urlRecherche: 'https://api.openweathermap.org/data/2.5/weather?'
      }
    },
    methods: {
      goMeteo(){
        axios.get(`${this.urlRecherche}q=${this.requete}&units=metric&APPID=${this.apiCode}&lang=fr`)
              .then(reponse => {
                this.temps = reponse.data
              })
        this.requete = '' 
      }
    }
  }
</script>

<style scoped>
  .texte-affichage {
    font-size: 30px;
    font-weight: 200;
    line-height: 1.2;
  }
</style>