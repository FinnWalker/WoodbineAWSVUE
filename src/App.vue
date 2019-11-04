<template>
  <div id="app">
    <table class="table table-bordered" style="border-collapse: collapse">
      <thead>
        <th colspan="3" style="text-align: center">
          <h1>
            <img
              src="./assets/images/woodbine.jpg"
              style="height:7.1vmin; position:relative; top: -0.5vmin"
            /> TURF CLUB
            <br />LEADERBOARD
          </h1>
        </th>
        <tr>
          <th style="color: rgb(227, 39, 38)">JOCKEY</th>
          <th style="color: rgb(227, 39, 38)">HORSE</th>
          <th style="color: rgb(227, 39, 38)">TIME</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="player in leaderboard" :key="player.name">
          <td>{{player.name}}</td>
          <td>
            {{horseName(player.horse)}}
            <img :src="require(`@/assets/images/${player.horse}.png`)" />
          </td>
          <td>{{convertTime(player.time)}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
const axios = require("axios");
//const uuid = require("uuid");

export default {
  name: "app",
  data: function() {
    return {
      leaderboard: null
    };
  },
  components: {},
  methods: {
    convertTime(time) {
      const minutes = parseInt(time / 60);
      let seconds = time % 60;
      if (seconds < 10) {
        seconds = "0" + seconds.toFixed(2);
      } else {
        seconds = seconds.toFixed(2);
      }

      return minutes + ":" + seconds;
    },
    horseName(horse) {
      switch (horse) {
        case 0:
          return "Betty Runs";

        case 1:
          return "Out Of The Blue";

        case 2:
          return "Early Bird";

        case 3:
          return "Encore Again";

        case 4:
          return "Epic Taste";

        case 5:
          return "Girls Night Out";

        case 6:
          return "Hotline Bling Bling";

        case 7:
          return "Shot In The Dark";

        case 8:
          return "I Spot A Tiger";

        case 9:
          return "Maple Leaf Madness";

        case 10:
          return "Mum's The Word";

        case 11:
          return "Reel Action";

        case 12:
          return "Sam Sung A Song";

        case 13:
          return "Shadow Lily";

        case 14:
          return "Started From The Middle";

        case 15:
          return "Usain Colt";

        default:
          return "";
      }
    }
  },
  mounted() {
    const options = {
      method: "GET",
      headers: {
        "content-type": "application/x-www-form-urlencoded"
      },
      url: "https://shoreportal.com/WoodbineAWS/leaderboard/get"
    };
    axios(options).then(response => {
      this.leaderboard = response.data;
    });
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

@font-face {
  font-family: EuclidFlex-Regular;
  src: url(./assets/fonts/EuclidFlex-Regular.otf);
}

@font-face {
  font-family: EuclidFlex-Bold;
  src: url(./assets/fonts/EuclidFlex-Bold.otf);
}
.table thead th {
  border: 1px solid black;
}
table.table-bordered > thead > tr > th {
  border: 1px solid black;
  text-align: left;
}
table.table-bordered > tbody > tr > td {
  border: 1px solid black;
  text-align: left;
}
table.table-bordered {
  border: 1px solid black;
}

th {
  font-family: EuclidFlex-Bold;
  font-size: 3vmin;
}
td {
  font-family: EuclidFlex-Bold;
  font-size: 3vmin;
}
h1 {
  font-family: EuclidFlex-Bold;
  text-align: center;
  font-size: 4vmin;
  color: #232020;
}
td img {
  height: 4.5vmin;
  float: right;
}
</style>
