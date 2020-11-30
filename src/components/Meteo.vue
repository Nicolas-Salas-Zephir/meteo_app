<template>
  <div class="container">
    <div class="form-group mb-5 pt-5">
      <!-- <label for="position">Entrer le nom d'une ville</label> -->
      <input 
        type="text" 
        id="position" 
        class="form-control"
        v-model='requete'
        @keypress.enter='goMeteo'
        placeholder="Rechercher une ville"
      />
    </div>
    <main v-if="time" class="w75 m-auto">
        <section class="main-info">
          <div class="row">
            <div class="col-12">
              <h1 class="text-center">{{ time.name }} </h1>
            </div>
          </div>
          <div class="row justify-content-end">
            <div class="col-5 text-left">
                <p class="text-affichage mb-0">
                    {{ time.main.temp.toFixed() }}°C
                </p>
                <p class="text-affichage mb-0">
                    {{ time.weather[0].description }}
                </p>
            </div>
          </div>
          <div class="row justify-content-start">
            <div class="col-8 p-1 text-right">
                <img src="../../public/images/soleil.png" alt="">
            </div>
          </div>
        </section>
        <section class="secondary-info">
          <div class="row">
            <div class="col-6 pr-1">
              <div class="item">
                <p>Taux d'humidité</p>
              </div>
              <div class="item-info text-center">
                <p> {{ time.main.humidity }}% </p>
              </div>
            </div>
            <div class="col-6 pl-1">
              <div class="item">
                <p>Température ressentie</p>
              </div>
              <div class="item-info text-center">
                <p>55%</p>
              </div>
            </div>
          </div>
        </section>
        <section class="prevision">
          <div class="row">
            <div class="col-4 pr-1">
              <div class="item-prev">
                <img src="../../public/images/soleil.png" alt="">
                <p>30°C</p>
              </div>
            </div>
            <div class="col-4 pr-1 pl-1">
              <div class="item-prev">
                <img src="../../public/images/soleil.png" alt="">
                <p>30°C</p>
              </div>
            </div>
            <div class="col-4 pl-1">
              <div class="item-prev">
                <img src="../../public/images/soleil.png" alt="">
                <p>30°C</p>
              </div>
            </div>
          </div>
        </section>
    </main>
    
  </div>
</template>

<script>
import axios from 'axios'


export default {
  name: "Meteo",
  data() {
      return {
          requete: '',
          time: undefined,
          api_code: 'cf360cb9a12f6a24c18517e00ecd6e78',
          url_search: 'https://api.openweathermap.org/data/2.5/weather?'
      }
  },
  methods: {
      goMeteo() {
            axios
                .get(`${this.url_search}q=${this.requete}&units=metric&appid=${this.api_code}&lang=fr`)
                .then(response => {
                this.time = response.data
                console.log(this.time)
            })
            this.requete = ""
      }
  }
};
</script>


<style scoped>

  input[placeholder] {
    font-weight: 300;
    color: #C6C6C6;
    box-shadow: 1px 6px 6px 0px #05696C;
  }

  h1 {
    font-weight: 900;
    font-size: 74px;
    color: #fff;
  }

  .main-info {
    margin-bottom: 25vw;
  }

  .main-info p {
    font-size: 19px;
  }

  .secondary-info .item {
    background-color: rgba(255,255,255,0.35);
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 9px;
    border-radius: 3px;
    box-shadow: 1px 6px 6px 0px #05696C;
    margin-bottom: 4vw;
  }

  .secondary-info {
    margin-bottom: 15vw;
  }

  .secondary-info .item p {
    font-size: 13px;
  }

  .secondary-info .item-info {
    font-size: 34px;
  }

  .secondary-info .item p, .secondary-info .item-info p {
    margin-bottom: 0 !important;
  }

  .prevision .item-prev {
    position: relative;
    display: flex;
    align-items: flex-end;
    justify-content: flex-end;
    background-color: rgba(255,255,255,0.35);
    border-radius: 3px;
    height: 88px;
  }

  .prevision .item-prev p {
    font-size: 23px;
    margin: 0 10px 5px 0;
  }

  .prevision .item-prev img {
    position: absolute;
    top: -20px;
    width: 87px;
  }

</style>