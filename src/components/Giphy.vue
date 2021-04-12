<template>
  <div class="container">
    <input type="text" name="query" placeholder="Cherhcer..." v-model="query" autocomplete="off">
    <h1>Bienvenue sur Ghiphy-gen</h1>
    <p>Rechercher et télécharger des gifs qui vous feront rire</p>
    <button @click="download">click</button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Giphy',
  data () {
    return {
      query: '',
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
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  width: 90%;
  margin: auto;
  margin-top: 60px;
}

input {
  height: 45px;
  width: 90%;
  margin: auto;
  border: none;
  border-radius: 8px;
  box-shadow:  44px 44px 76px #b8bbbe,
             -44px -44px 76px #ffffff;
}
</style>
