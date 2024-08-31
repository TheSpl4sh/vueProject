<script>
import axios from 'axios'
    export default {
      data() {
        return {
          city: "",
          error: "",
          info: null
        }
      },
      computed: {
        cityName() {
          return "«" + this.city + "»"
        },
        showTemp() {
          return "Temperature: " + this.info.main.temp
        },
        showFeelsLike() {
          return "Feels like: " + this.info.main.feels_like
        },
        showMinTemp() {
          return "Minimal temperature: " + this.info.main.temp_min
        },
        showMaxTemp() {
          return "Maximum temperature: " + this.info.main.temp_max
        },
      },
      methods: {
        getWeather() {
          this.info = null

          if(this.city.trim().length < 2) {
            this.error = "Need more than 1 symbol"
            return false
          }

          this.error = ""

          axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=8ae705b2f3de7175cdafa1fcfcc4cf31`)
            .then(res => (this.info = res.data))
            .catch(error => {
              if(error.status == 404 ) {
                this.error = "Incorrect city name"
              }
            })
        }
      }
    }
</script>

<template>
    <div class="wrapper">
      <header>
        <h1>Weather app </h1>
        <p>Find out the weather in {{ city == ""?" your city" : cityName }}</p>
        <input type="text" v-model="city" placeholder="Enter city">
        <button v-if="city != ''" @click="getWeather()">Get the weather</button>
        <button disabled v-else="city != ''">Enter city name</button>
        <p class="error"> {{ error }}</p>

        <section v-if="info != null">
          <p >{{ showTemp }}</p>
          <p >{{ showFeelsLike }}</p>
          <p >{{ showMinTemp }}</p>
          <p >{{ showMaxTemp }}</p>


        </section>
      </header>
    </div>
</template>


<style scoped>
.error {
  color: red;
}

.wrapper {
  max-width: 1368px;
  padding: 30px;
}

header {
  max-width: 700px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background-color: #20223b;
  color: #dddddd;
  text-align: center;
}

header p {
  margin-top: 20px;
}

h1 {
  margin-top: 50px;
}

header input {
  margin-top: 30px;
  background-color: transparent;
  border: 0;
  border-bottom: 2px solid #20223b;
  color: #dddddd;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
  transition: border-bottom-color 0.3s ease;
}

header input:focus {
  border-bottom-color: white;
}

header button {
  background-color: #42a232;
  color: white;
  border-radius: 10px;
  border: 2px solid white;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}
 
header button:disabled {
  background-color: #8f7c25;
  cursor: not-allowed;
}

header button:hover {
  transform: scale(1.1) translate(-5px);
}

@media(min-width: 768px) {
  .wrapper {
    max-width: 100%;
  }

  header {
    margin: auto;
  }
}

</style>
