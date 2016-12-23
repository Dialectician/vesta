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
      // axios.get('http://192.168.1.8/cgi-bin/ctlJsonDump?header=1&start=1482445963')
      this.$http.get('/api/data/elements_v2.csv')
        .then(function (response) {
          var lines = response.body.split('\n')
          var data = {}
          var headings = lines[0].split(',').map(function (heading) {
            return heading.replace(/"/g, '')
          })
          headings.shift()
          lines.shift()
          for (var l in lines) {
            var line = lines[l].trim()
            var items = line.split(',')
            if (items.length > 5) {
              items.shift()
              var name = items[5].replace(/"/g, '')
              items.splice(5, 1)
              var obj = {}
              for (var i in items) {
                var item = items[i]
                if (item[0] === '"') {
                  item = item.replace(/"/g, '')
                } else if (item.indexOf('.') > -1) {
                  item = parseFloat(item)
                } else {
                  item = parseInt(item)
                }
                obj[headings[i]] = item
              }
              data[name] = obj
            }
          }
          console.log(data)
          console.log(data['DHW'].value)
          this.tempdata = data
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
