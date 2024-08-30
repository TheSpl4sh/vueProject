<script>
    export default {
      data() {
        return {
          city: "",
          errors: ""
        }
      },
      computed: {
        cityName() {
          return "«" + this.city + "»"
        }
      },
      methods: {
        getWeather() {
          if(this.city.trim().length < 2)

          return false
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
      </header>
    </div>
</template>


<style scoped>
.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background-color: #20223b;
  color: #dddddd;
  text-align: center;
}

.wrapper p {
  margin-top: 20px;
}

h1 {
  margin-top: 50px;
}

.wrapper input {
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

.wrapper input:focus {
  border-bottom-color: white;
}

.wrapper button {
  background-color: #42a232;
  color: white;
  border-radius: 10px;
  border: 2px solid white;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}
 
.wrapper button:disabled {
  background-color: #8f7c25;
  cursor: not-allowed;
}

.wrapper button:hover {
  transform: scale(1.1) translate(-5px);
}

</style>
