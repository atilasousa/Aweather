<template>
  <div id="app">
    <div class="content">
      <div class="overlay">
        <section class="left">
          <header>
            <img src="../public/assets/logo.png" alt="Logo-Aweather" />
          </header>
          <div class="searchboxg mobile">
            <input
              type="text"
              class="searchtext"
              v-model="searchtext"
              placeholder="Insira o nome da sua cidade aqui..."
              @keypress="getweather"
            />
          </div>
          <main
            class="cityTempHolder"
            v-if="typeof weather.main != 'undefined'"
          >
            <div class="cityTemp">
              <div class="cityDate desk">
                <h1>{{ weather.name }}, {{ weather.sys.country }}</h1>
                <p>{{ dateBuilder() }}</p>
              </div>
              <div class="temp">
                <h1 class="mobile">
                  {{ Math.round(weather.main.temp) }}°C {{ weather.name }},
                  {{ weather.sys.country }}
                </h1>
                <p class="mobile">{{ dateBuilder() }}</p>
                <h1 class="desk">{{ Math.round(weather.main.temp) }}°C</h1>
              </div>
            </div>
            <div class="weathericon">
              <i class="fas fa-cloud"></i>
              <span>Clouds</span>
            </div>
          </main>
        </section>
        <section class="right">
          <div class="searchboxg desk">
            <input
              type="text"
              class="searchtext"
              v-model="searchtext"
              placeholder="Insira o nome da sua cidade aqui..."
              @keypress="getweather"
            />
          </div>
          <div class="detailsbox" v-if="typeof weather.main != 'undefined'">
            <span>Detalhes do tempo</span>
            <hr class="line" />
            <span class="details">Humidade: {{ weather.main.humidity }}% </span>
            <span class="details">Vento: {{ weather.wind.speed }} km/h</span>
          </div>
          <footer class="rightfooter">
            <span>© {{ year }} Aweather. All rights reserved.</span>
          </footer>
        </section>
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
          `${this.url}weather?q=${this.searchtext}&units=metric&lang=pt&APPID=${this.api_key}`
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
      return `${dia}, ${data} de ${mes} de ${ano}`;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.mobile {
  display: none;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.content {
  width: 100vw;
  height: 100vh;
  background-image: url("../public/assets/weather.jpg");
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
}
.overlay {
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.493);
  display: flex;
}
.left {
  width: 60%;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}

.left header {
  position: absolute;
  z-index: 10;
  top: 0;
  left: 0;
  width: 100%;
  padding: 20px;
}
.left header img {
  width: 80px;
}
.cityTempHolder {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  color: white;
}
.weathericon {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.weathericon i {
  font-size: 3rem;
}
.weathericon span {
  font-size: 1.5rem;
  font-weight: bold;
}
.cityTemp {
  width: 60%;
 
  height: 150px;
  border-radius: 15px;
  display: flex;
  flex-direction: row-reverse;
  justify-content: center;
}
.cityDate {
  margin-left: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.cityDate h1 {
  font-size: 2.2rem;
}
.cityDate p {
  font-size: 0.9rem;
}
.temp {
  display: flex;
  justify-content: center;
  align-items: center;
}
.temp h1 {
  font-size: 4rem;
}

.searchboxg {
  width: 80%;
  height: 50px;
  background-color: none;
  margin-top: 30px;
  transition: 0.3s;
}
.searchtext {
  height: 100%;
  width: 100%;
  padding-left: 20px;
  outline: none;
  border: none;
  background-color: rgba(255, 255, 255, 0.616);
  border-radius: 0px 15px 0px 15px;
  transition: 0.3s;
}
.searchtext:focus {
  border-radius: 15px 0px 15px 0px;
  background-color: rgba(255, 255, 255, 0.849);
}
.line {
  width: 100%;
  border: none;
  height: 0.1px;
  background-color: rgba(250, 249, 249, 0.712);
  margin-top: 10px;
}
.detailsbox {
  color: white;
  width: 80%;
  margin-top: 40px;
  display: flex;
  flex-direction: column;
  transition: 0.3s;
}
.detailsbox :first-child {
  font-size: 1.3rem;
}
.details {
  margin-top: 13px;
  font-size: 1.1rem;
}
.right {
  width: 40%;
  height: 100%;
  background-color: #3d5663b2;
  border-radius: 15px 0 0 15px;
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: baseline;
  position: relative;
}
.rightfooter {
  position: absolute;
  bottom: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  padding: 20px;
  width: 100%;
}
@media only screen and (max-width: 900px) {
  .desk {
    display: none;
  }
  .mobile {
    display: block;
  }
  .content{
    height: 100vh;
  }
  .overlay {
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    
  }
  .left {
    width: 100%;
    position: relative;
    top: 0;
    left: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    
  }
  .left header {
    position: relative;
    z-index: 10;
    width: 100%;
    
    padding: 10px;
  }
  .left header img {
    width: 60px;
  }
  .cityTempHolder {

    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
    margin-bottom: 20px;
    margin-top: 20px;
  }
  .cityTemp {
    width: 80%;
    padding: 10px;
    height: auto;
    flex-wrap: wrap;
    flex-direction: row-reverse;
    justify-content: space-around;
    
  }
  
  .cityDate h1 {
    font-size: 1.5rem;
  }
  .temp {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    width: 100%;
  }
  .temp h1 {
    font-size: 2rem;
  }
  .right {
    height: auto;
    width: 80%;
    border-radius: 15px;
  }
  .rightfooter {
    position: relative;
    
  }
  .rightfooter span {
    font-size: 0.9rem;
  }
}
</style>