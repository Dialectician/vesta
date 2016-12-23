<template>
  <div class="temperature">

    <h2>Vesta Controller</h2>
    <button class="btn btn-danger" v-on:click="fetchvdata(this.vdata)">GET</button>
    
    <h4>
  {{tempdata}}
</h4>
  </div>
</template>

<script>
//  import axios from 'axios'

export default {
  name: 'temperature',
  data () {
    return {
      tempdata: []

    }
  },

  ready: function () {
    this.fetchvdata()
  },

  methods: {

    fetchvdata: function () {
      // var ddd = new Date()
      // var secondsMinus = Math.round(ddd.getTime() / 1000 - 60)
      //
      // this.$http.get('http://192.168.1.8/cgi-bin/ctlJsonDump?head=0&start=' + secondsMinus)
  //    axios.get('http://192.168.1.8/cgi-bin/ctlJsonDump?header=1&start=1482445963')
      this.$http.get('http://192.168.1.8:7280/?div=nw002&get=2;div=nw003&get=3;div=nw004&get=4;div=nw005&get=5;div=nw006&get=6;div=nw007&get=8;div=nw008&get=9;div=nw009&get=14;div=nw010&get=15;div=nw011&get=17;div=nw012&get=18;div=nw013&get=19;div=nw014&get=20;div=nw015&get=21;div=nw017&get=10;div=nw019&get=57;div=nw020&get=56;div=nw021&get=27;div=nw022&get=26;div=nw023&get=28;div=nw025&get=62;div=nw026&get=63;div=nw027&get=64;div=nw028&get=65;div=nw029&get=58;div=nw030&get=59;div=nw031&get=60;div=nw033&get=104;div=nw034&get=105;div=nw035&get=146;div=nw036&get=144;div=nw037&get=145;div=nw038&get=143;div=nw039&get=141;div=nw040&get=140;div=nw041&get=139;div=nw042&get=138;div=nw043&get=136;div=nw044&get=132;div=nw045&get=126;div=nw046&get=125;div=nw047&get=124;div=nw048&get=123;div=nw049&get=121;div=nw050&get=115;div=nw051&get=114;div=nw052&get=113;div=nw053&get=112;div=nw054&get=110;div=nw055&get=109;div=nw056&get=108;div=nw057&get=107;div=nw059&get=106;div=nw060&get=111;div=nw061&get=116;div=nw062&get=117;div=nw063&get=118;div=nw064&get=119;div=nw065&get=120;div=nw066&get=122;div=nw067&get=127;div=nw068&get=128;div=nw069&get=129;div=nw070&get=130;div=nw071&get=134;div=nw072&get=131;div=nw073&get=135;div=nw074&get=137;div=nw075&get=142')
        .then(function (response) {
          var rb = response.body
          var rbSplit = []
          var to = rb
          var toSplit = to.split(/\r|\n/)
          for (var i = 0; i < toSplit.length; i++) {
            rbSplit.push({'vestaobj': toSplit[i]})
          }

          this.tempdata = rbSplit
        })
        .catch(function (error) {
          console.log(error)
          console.log(window.location.search)
        })
    }
  }
}
//   created: function () {
//     this.fetchvdata(this)
//   }
// }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
</style>
