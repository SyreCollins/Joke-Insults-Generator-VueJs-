<template>
  <div class="main" v-if="showOther">
    <h2>* Syre's Insult Generator *</h2>
    <div class="display-area">
      <i id="text">{{ InsultText }}</i>
    </div>
    <button @click="generateInsult">Generate</button>
  </div>

  <div class="col" v-else>
    <h2>* Syre's Joke Generator *</h2>
    <div class="display-area">
      <i id="txt">{{ JokeText }}</i>
    </div>
    <button @click="generateJoke">Generate</button>
  </div>
  <div class="nothing"></div>
  <b @click="switchGen">Switch to Joke/Insult Generator.</b>
</template>

<script>

export default {
  name: 'App',
  components: {
    
  },
  data() {
    return {
      showOther: true,
      JokeText: 'Joke would be displayed here.',
      InsultText: 'Insult would be displayed here.'
    }
  },
  methods: {
    generateInsult() {
      console.log('fetching..')
      fetch('https://insult.mattbas.org/api/insult')
      .then((data) => data.text())
      .then((output) => this.InsultText = output)
      .catch(err => console.log(err.message))
    },
    generateJoke() {
      console.log('fetching...')
      fetch('https://v2.jokeapi.dev/joke/Any')
      .then((data) => data.json())
      .then((output) => {
        if(output.type = 'single') {
          if(output.joke) {
            this.JokeText = output.joke
          } else {
            this.JokeText = output.setup + '' + output.delivery
          }
        }
        console.log(output)
      })
      .catch(err => console.log(err.message))
    },
    switchGen() {
      this.showOther = !this.showOther
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Nunito+Sans:ital,wght@1,300&display=swap');
body {
  background-color: #222;
}
#app {
  font-family: 'Nunito Sans', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
.main, .col {
  max-width: 75%;
  margin: 0 auto;
  margin-top: 20px;
  color: #fff;
}
.display-area {
  width: 220px;
  height: 100px;
  margin: 0 auto;
  background-color: #111;
  color: #777;
  border-radius: 3.2px;
  padding: 8px;
  margin-top: 7.2px;
  line-break: auto;
}
.main button, .col button {
  background-color: #333;
  outline: none;
  width: 240px;
  height: 45px;
  border: none;
  border-radius: 5px;
  color: #fff;
  margin-top: 10px;
}
.nothing {
  height: 70px;
}
b {
  cursor: pointer;
  text-decoration: underline;
  color: beige;
  letter-spacing: 1px;
  line-height: 1.5px;
  font-size: small;
}
</style>
