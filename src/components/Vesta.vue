<template>
  <div class="temperature">

    <h2>Vesta Controller</h2>
    <button class="btn btn-danger" v-on:click="fetchvdata(this.vdata)">GET Temps</button>

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
      this.$http.get('http://206.53.94.183/public/ctlpanel.txt')
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
        })
    }
  }
}

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
button {
  border-color: black;
    border-top-color: black;
    border-right-color: black;
    border-bottom-color: black;
    border-left-color: black;
}


</style>
