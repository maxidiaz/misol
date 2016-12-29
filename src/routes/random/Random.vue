<template lang="html">
  <div>
    <div>
      <img :src="randomGif" alt="" class="random-gif" v-on:load="$hideSpinner()">
    </div>
    <div class="card otra-btn margin16" v-on:click="getRandomGif()">Otra</div>
  </div>
</template>

<script>
export default {
  name: 'random',
  data () {
    return {
      randomGif: ''
    }
  },
  created () {
    this.getRandomGif()
  },
  methods: {
    getRandomGif () {
      const self = this
      this.$showSpinner()
      this.$http.get('http://api.giphy.com/v1/gifs/random?api_key=dc6zaTOxFJmzC').then(response => {
        self.randomGif = response.data.data.image_original_url
      }).catch(err => {
        self.$hideSpinner()
        self.$displayDialog('Lo siento...', 'Hubo un inconveniente. Intentá más tarde', ()=>{
          self.$router.back()
        })
      })
    }
  }
}
</script>

<style lang="css">
.otra-btn {
  background-color: #337ab7;
  color: white;
  font-size: 20px;
  padding: 10px;
  margin-top: 16px;
}

.random-gif {
  max-width: 100%;
  display: block;
  margin: 16px auto;
}
</style>
