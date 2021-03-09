<template>
  <div id="app">
    <div class="content">
      <div class="overlay">
        <div class="LeftDiv">
          <header>
            <img src="../public/assets/logo.png" width="80px" alt="" />
          </header>
          <div style="margin: 20px">
            <h1>Luanda, AO</h1>
            <p>Sunday 26 August 2020</p>
          </div>
          <div class="centerContent">
            <h1 style="color: white; font-size: 4rem">16°C</h1>
          </div>
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
          <div class="detailsbox">
            <p class="details-text">Detalhes do tempo</p>
            <hr class="line" />
            <p class="details-text">Precipitação: 100%</p>
            <p class="details-text">Humidade: 100%</p>
            <p class="details-text">Vento: 100%</p>
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
      url:'api.openweathermap.org/data/2.5',
      year: new Date().getFullYear(),
      searchtext:'',
      weather:{}
    };
  },
  methods: {
    
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
  justify-content: center;
  align-items: center;
  flex-direction: column;
  color: white;
}
.LeftDiv header {
  position: absolute;
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
  width: 200px;
  height: 200px;
  border: none;
  background-color: #3d56639f;
  border-radius: 15px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  color: white;
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
  padding: 10px;
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
</style>
