<template>
  <div class="hello">
    <br />
    <h1>
      {{ msg }}
    </h1>
    <button class="button" @click="randomOpeningNumber()">
      Random opening
    </button>
    <p>
      {{ opening[randomNumber].Name }}
    </p>
    <p>
      {{ opening[randomNumber].Pgn }}
    </p>
  </div>
  <footer id="footer">
    <div>
      Icons made by
      <a href="https://www.freepik.com" title="Freepik">Freepik</a> from
      <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a>
    </div>
  </footer>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      opening: [
        {
          Eco: "A00",
          Name: "Amar Gambit",
          Pgn: "1. Nh3 d5 2. g3 e5 3. f4 Bxh3 4. Bxh3 exf4",
          Uci: "g1h3 d7d5 g2g3 e7e5 f2f4 c8h3 f1h3 e5f4",
          Epd: "rn1qkbnr/ppp2ppp/8/3p4/5p2/6PB/PPPPP2P/RNBQK2R w KQkq -",
        },
      ],
      randomNumber: 0,
    };
  },
  async created() {
    // GET request using axios with async/await
    const response = await axios.get(
      "https://europe-west3-static-potion-161608.cloudfunctions.net/random-chess-opening-api"
    );
    this.opening = response.data;
  },
  methods: {
    randomOpeningNumber: function () {
      this.randomNumber = Math.floor(Math.random() * 3396 + 1); //multiply to generate random number between 0, 100
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
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

#footer {
  background-color: #f3e5f5;
  padding: 20px;
}

.button {
  position: relative;
  background-color: #4caf50;
  border: none;
  font-size: 28px;
  color: #ffffff;
  padding: 20px;
  width: 200px;
  text-align: center;
  transition-duration: 0.4s;
  text-decoration: none;
  overflow: hidden;
  cursor: pointer;
}

.button:after {
  content: "";
  background: #f1f1f1;
  display: block;
  position: absolute;
  padding-top: 300%;
  padding-left: 350%;
  margin-left: -20px !important;
  margin-top: -120%;
  opacity: 0;
  transition: all 0.8s;
}

.button:active:after {
  padding: 0;
  margin: 0;
  opacity: 1;
  transition: 0s;
}
</style>
