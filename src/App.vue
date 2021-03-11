<template>
  <div id="app">
    <div class="content">
      <div class="overlay">
        <div class="LeftDiv">
          <header>
            <img src="../public/assets/logo.png" width="80px" />
          </header>
          <div class="searchboxmobile">
            <input
              type="text"
              placeholder="Insira aqui o nome da sua cidade..."
              class="searchinput"
              v-model="searchtext"
              @keypress="getweather"
            />
          </div>
          <div class="centerContent" v-if="typeof weather.main != 'undefined'">
            <h1 class="h1city">
              {{ weather.name }}, {{ weather.sys.country }}
            </h1>
            <p>{{ dateBuilder() }}</p>
            <h1 class="h1temp" style="color: white">
              {{ Math.round(weather.main.temp) }}°C
            </h1>
          </div>
          <h1
            class="centerContent2"
            style="margin-top: 10px"
            v-if="typeof weather.main != 'undefined'"
          >
            {{ weather.weather[0].main }}
          </h1>
        </div>
        <div class="RightDiv">
          <div class="searchbox">
            <input
              type="text"
              placeholder="Insira aqui o nome da sua cidade..."
              class="searchinput"
              v-model="searchtext"
              @keypress="getweather"
            />
          </div>
          <div class="detailsbox" v-if="typeof weather.main != 'undefined'">
            <p class="details-text">Detalhes do tempo</p>
            <hr class="line" />

            <p class="details-text">Humidade: {{ weather.main.humidity }}%</p>
            <p class="details-text">Vento: {{ weather.wind.speed }} km/h</p>
          </div>
          <footer>
            <p>© {{ year }} Aweather. All rights reserved.</p>
          </footer>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "88bda33f4889ae5dab3a5116b34f856c",
      url: "https://api.openweathermap.org/data/2.5/",
      year: new Date().getFullYear(),
      searchtext: "",

      weather: {},
    };
  },
  methods: {
    getweather(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.url}weather?q=${this.searchtext}&units=metric&lang=pt_br&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.results);
      }
    },
    results(results) {
      if (results.cod == "404") {
        this.searchtext = "";
        alert("Cidade não encontrada");
        this.weather = {};
      } else {
        this.searchtext = "";
        this.weather = results;
      }
    },
    dateBuilder() {
      let date = new Date();
      let meses = [
        "Janeiro",
        "Fevereiro",
        "Março",
        "Abril",
        "Maio",
        "Junho",
        "Julho",
        "Agosto",
        "Setembro",
        "Outubro",
        "Novembro",
        "Dezembro",
      ];
      let dias = [
        "Domingo",
        "Segunda-feira",
        "Terça-Feira",
        "Quarta-feira",
        "Quinta-feira",
        "Sexta-feira",
        "Sábado",
      ];
      let dia = dias[date.getDay()];
      let data = date.getDate();
      let mes = meses[date.getMonth()];
      let ano = this.year;
      return `${dia} ${data} de ${mes} de ${ano}`;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.content {
  background-image: url("../public/assets/weather.jpg");
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
  width: 100vw;
  height: 100vh;
  position: relative;
}
.LeftDiv {
  width: 60%;
  height: 100%;
  position: relative;
  display: flex;
  flex-direction: column;
  color: white;
  align-items: center;
}
.LeftDiv header {
  position: relative;
  width: 100%;
  z-index: 2;
  top: 0;
  left: 0;
  display: flex;
  align-items: flex-start;
  padding-left: 20px;
  padding-top: 20px;
}
.centerContent {
  width: 300px;
  height: 200px;
  border: none;
  background-color: #3d56639f;
  border-radius: 15px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  color: white;
  transition: 0.3s;
}
.centerContent h1 {
  margin: 10px;
}
.h1temp {
  font-size: 4rem;
}
.RightDiv {
  width: 40%;
  height: 100%;
  background-color: #3d56639f;
  color: white;
  position: relative;
}
.RightDiv footer {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  color: rgba(209, 209, 209, 0.863);
  padding: 10px;
}
.searchbox {
  padding: 20px 50px 20px 50px;
  border: none;
}
.searchinput {
  width: 100%;
  height: 36px;
  padding: 22px;
  background: none;
  border: none;
  background-color: rgba(255, 255, 255, 0.856);
  outline: none;
  transition: 0.3s;
  border-radius: 0 15px 0 15px;
}
.searchinput:focus {
  background-color: rgb(255, 255, 255);
  border-radius: 15px 0 15px 0;
}
.line {
  width: 100%;
  border: none;
  height: 0.1px;
  background-color: rgba(250, 249, 249, 0.712);
}
.details-text {
  margin: 10px 0 10px 0;
  font-size: 1.2rem;
}
.detailsbox {
  padding: 50px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  transition: 0.3s;
}
.overlay {
  position: absolute;
  z-index: 2;
  background-color: rgba(0, 0, 0, 0.651);
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: space-between;
}

@media only screen and (max-width: 900px) {
  .overlay {
    flex-direction: column;
    align-items: center;
  }
  .RightDiv {
    width: 80%;
    height: 300px;
    border-radius: 15px;
  }
  .centerContent {
    margin-top: 40px;
    width: 80%;
    height: 150px;
  }
  .h1city {
    font-size: 2rem;
  }
  .h1temp {
    font-size: 2.5rem;
  }
  .searchbox {
    display: none;
  }
  .LeftDiv header {
    width: 100%;
    align-items: center;
    justify-content: center;
    padding-top: 20px;
  }
  .searchboxmobile{
    width: 80%;
    margin-top: 40px;
  }
  .LeftDiv{
    width: 100%;
  }
}
@media only screen and (min-width: 901px) {
 .searchboxmobile{
   display: none;
 }
}
</style>
