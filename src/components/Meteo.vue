<template>
  <div class="container">
    <h1 class="my-4">App Meteo avec Vue.js</h1>
    <div class="form-group mb-5">
      <label for="position">Entrer le nom d'une ville</label>
      <input 
        type="text" 
        id="position" 
        class="form-control"
        v-model='requete'
        @keypress.enter='goMeteo'
      />
    </div>
    <div v-if="temps" class="w75 m-auto">
        <h3 class="text-center">Position : {{ temps.name }} </h3>
        <div class="card text-center p-5">
            <p class="text-affichage">
                temperature : {{ temps.main.temp.toFixed() }}
            </p>
            <p class="text-affichage">
                Temps : {{ temps.weather[0].description }}
            </p>
        </div>
    </div>
    
  </div>
</template>

<script>
import axios from 'axios'


export default {
  name: "Meteo",
  data() {
      return {
          requete: '',
          temps: undefined,
          api_code: 'cf360cb9a12f6a24c18517e00ecd6e78',
          url_recherche: 'https://api.openweathermap.org/data/2.5/weather?'
      }
  },
  methods: {
      goMeteo() {
            axios
                .get(`${this.url_recherche}q=${this.requete}&units=metric&appid=${this.api_code}&lang=fr`)
                .then(response => {
                
                this.temps = response.data
                console.log(this.temps)
                
            })
            this.requete = ""
      }
  }
};
</script>


<style>
</style>