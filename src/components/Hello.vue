<template>
  <div class="temperature">
    <h1 class="page-header">{{this.vdata}}
    <h2>Essential Links</h2>
    <button class="btn btn-danger" v-on:click="fetchvdata(this.vdata)">GET</button>
    <h2>Ecosystem</h2>
  </div>
</template>

<script>
export default {
  name: 'temperature',
  data () {
    return {
      tempdata: ''
    }
  },
  methods: {
    fetchvdata () {
      this.$http.get('http://192.168.1.8:7280/?div=nw002&get=02')
        .then(function (response) {
          this.vdata = JSON.parse(response.body)
        })
    }
  },
  created: function () {
    this.fetchvdata(this)
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
</style>
