<template>
  <div class="hello">
    <button @click="download">click</button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Giphy',
  data () {
    return {
      query: 'coconut',
      api_key: '1CGNJI8lyPAbgiZdoJ5844P14yPrRd4F',
      base_url: 'https://api.giphy.com/v1/gifs/search?api_key=${api_key}&q=${query}&limit=25&offset=0&rating=g&lang=en',
      load: ''
    }
  },
  created () {
    axios({
        url: `https://api.giphy.com/v1/gifs/search?api_key=${this.api_key}&q=${this.query}&limit=25&offset=0&rating=g&lang=en`,
        method: 'GET',
      }).then(response => {
        // const url = window.URL.createObjectURL(new Blob([response.data]))
        this.load = response.data.data[0].images.original.url
        console.log(this.load)
      })
  },
  methods: {
    download () {
      axios({
        url: `${this.load}`,
        method: 'GET',
        responseType: 'blob'
      }).then(response => {
        const url = window.URL.createObjectURL(new Blob([response.data]))
        const link = document.createElement('a')
        link.href = url
        link.setAttribute("download", 'file.gif')
        document.body.appendChild(link)
        link.click()
        // console.log(response.data)
      })
    }
  }
}
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
</style>
