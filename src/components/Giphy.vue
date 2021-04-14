<template>
  <div class="container giphy">
    <div class="search_box">
      <input type="text" name="query" placeholder="Cherhcer..." v-model="query" autocomplete="off" @keypress="fetchGif">
    </div>
    <!-- About giphy-gen box -->
    <div class="about_box" v-if="show_about">
      <div class="about_content">
        <h1>Bienvenue sur Ghiphy-gen</h1>
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Quae harum obcaecati unde ipsam a quam voluptatem accusantium magni saepe quod.
        </p>
        <button @click="randomGif">
          <img src="@/assets/icon/arrow.svg" alt="arrow">
        </button>
      </div>
    </div>
    <!-- Loader -->
    <div class="loader" v-if="loader">
      <img src="@/assets/loader/tail-spin.svg" alt="data loader">
    </div>
    <!-- Trends gif animation -->
    <div class="random_gif" v-if="show_random">
      <h1>Gif populaire</h1>
      <div class="random_img" v-for="gif in load" :key="gif.id">
        <img :src="gif.images.original.url" :class="gif.title" alt="gif">
        <div class="radom_download" @click="download(gif)">
          <img src="@/assets/icon/download.svg" alt="download icon">
        </div>
        <!-- <p>{{ text(gif) }}</p> -->
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Giphy',
  data () {
    return {
      loader: false,
      show_about: true,
      show_random: false,
      query: '',
      api_key: '1CGNJI8lyPAbgiZdoJ5844P14yPrRd4F',
      base_url: 'https://api.giphy.com/v1/gifs/search?api_key=${api_key}&q=${query}&limit=25&offset=0&rating=g&lang=en',
      load: ''
    }
  },
  methods: {
    // TRENDS GIF FETCH
    randomGif () {
      this.loader = true
      axios({
        url: `https://api.giphy.com/v1/gifs/trending?api_key=${this.api_key}&limit=25&rating=g`,
        method: 'GET',
      }).then(response => {
        this.load = response.data.data
        this.loader = false
        this.show_random = true
        console.log("go fetch", this.load)
      })
      this.show_about = false
    },
    // TRENDS GIF TITLE
    // text (txt) {
    //   let title_text = ''
    //   let title = txt.title.split(' ').indexOf('GIF')
    //   for (let i = 0; i < title; i++) {
    //     title_text += txt.title.split(' ')[i] + ' '
    //   }
    //   return title_text
    // },
    // INPUT FETCH
    fetchGif () {
      axios({
        url: `https://api.giphy.com/v1/gifs/search?api_key=${this.api_key}&q=${this.query}&limit=25&offset=0&rating=g&lang=en`,
        method: 'GET',
      }).then(response => {
        this.load = response.data.data
        console.log("input fetch", this.load)
      })
    },
    // DOWNLOAD GIF
    download (base) {
      axios({
        url: `${base.images.original.url}`,
        method: 'GET',
        responseType: 'blob'
      }).then(response => {
        const url = window.URL.createObjectURL(new Blob([response.data]))
        const link = document.createElement('a')
        link.href = url
        link.setAttribute("download", `${base.title}.gif`)
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
  height: 100%;
  margin: 60px auto;
}

.search_box input {
  height: 60px;
  width: 90%;
  margin: auto;
  border: none;
  border-radius: 8px;
  background: linear-gradient(145deg, #d9dbdd, #ffffff);
  box-shadow:  11px 11px 22px #d2d3d6,
             -11px -11px 22px #ffffff;
  text-align: center;
  outline: none;
  text-transform: uppercase;
  color: #32373D;
  font-weight: bold;
  font-family: 'Poppins', sans-serif;
}

.search_box input::placeholder {
  color: #32373D;
}

.loader {
  width: 100%;
  height: 600px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.loader img {
  width: 100px;
}

.about_box {
  height: 600px;
  margin: auto;
  display: flex;
  align-items: center;
  justify-content: center;
}

.about_box .about_content {
  padding: 30px 15px;
  height: 400px;
  /* border: 2px solid #32373D; */
  border-radius: 8px;
  background: linear-gradient(145deg, #ffffff, #d9dbdd);
  box-shadow:  11px 11px 38px #d2d3d6,
             -11px -11px 38px #ffffff;
}

.about_box .about_content h1 {
  margin-top: 10px;
  text-transform: uppercase;
  line-height: 1em;
}

.about_box .about_content p {
  margin-top: 30px;
  color: #595A5D;
  font-weight: 500;
}

.about_box .about_content button {
  margin-top: 50px;
  width: 50px;
  height: 50px;
  border: none;
  outline: none;
  background: transparent;
}

.about_box .about_content button img {
  width: 50px;
  transform: rotate(90deg);
}

.random_gif {
  width: 100%;
  margin-top: 50px;
  display: flex;
  justify-content: space-around;
  align-items: center;
  flex-wrap: wrap;
}

.random_gif h1 {
  margin-top: 30px;
  margin-bottom: 25px;
  text-transform: uppercase;
  letter-spacing: -1px;
}

.random_gif .random_img {
  position: relative;
  margin: 22px 0;
  width: 160px;
  height: 280px;
  border: 3px solid #F4FAFF;
  padding: 10px;
  border-radius: 12px;
  background: #F1F3F6;
  box-shadow:  11px 11px 16px #e7e9ec,
             -11px -11px 16px #fbfdff;
}

.random_gif .random_img img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 10px;
}

.random_gif .random_img p {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 156px;
  height: 40px;
  margin-top: -30px;
  background-color: #141719;
  color: #fdffff;
  bottom: 0;
  border-bottom-right-radius: 11px;
  border-bottom-left-radius: 11px;
}

.random_gif .random_img .radom_download {
  position: absolute;
  padding: 10px;
  bottom: 10px;
  right: 10px;
  width: 45px;
  height: 45px;
  border: 2px solid black;
  border-radius: 12px;
  background: linear-gradient(315deg, #d7e7fd, #b5c2d4);
  box-shadow:  5px 5px 10px #cbdaee;
}

@media (max-width: 345px) {
  .random_gif .random_img {
    width: 200px;
  }

  .random_gif .random_img p {
    width: 198px;
  }
}
</style>
