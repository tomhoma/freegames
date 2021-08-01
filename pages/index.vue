<template>
<v-app>
  <v-container>
    <v-row>
      <v-col cols="8">
<v-row>
  <v-col v-for="item in gamesList" :key="item.id" cols='12'>
        <v-row>
          <v-col cols="3">
            <img :src="item.thumbnail" alt="" class="thumbnail"/>
          </v-col>
          <v-col cols="7">
            <nuxt-link :to="`/${item.id}`">
            <h1>{{ item.title }}</h1>
            </nuxt-link>
            <p>{{ item.short_description }}</p>
            <div class="genre">{{ item.genre }}</div>
          </v-col>
          <v-col cols="2" align-self="center">
            <!-- <div>{{ item.platform }}</div> -->
            <div class="d-flex">
            <svg v-if="isPlatformWindows(item.platform)" aria-hidden="true" focusable="false" data-prefix="fab" data-icon="windows" class="svg-inline--fa fa-windows fa-w-14 svg" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M0 93.7l183.6-25.3v177.4H0V93.7zm0 324.6l183.6 25.3V268.4H0v149.9zm203.8 28L448 480V268.4H203.8v177.9zm0-380.6v180.1H448V32L203.8 65.7z"></path></svg>
            <div>FREE</div>
            </div>
          </v-col>
        </v-row>  
      </v-col>
</v-row>
      </v-col>
      <v-col cols="4">
        <v-row>
          <v-col v-for="item in gamesList" :key="item.id" cols="12">
            <img :src="item.thumbnail" alt=""/>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</v-app>
</template>

<script>
export default {
  /*
  async asyncData({ context }) {
    context.$axios.get......
    } 
  */
  async asyncData({ $axios }) {
    const config = {
      "x-rapidapi-key": "bf42eb820cmsh1b4e9fb2ae3fe7dp1893f1jsn4d6ab01716e3",
      "x-rapidapi-host": "free-to-play-games-database.p.rapidapi.com"
    }
  const result = await $axios.get(
    "https://free-to-play-games-database.p.rapidapi.com/api/games",
    {
      headers: config
    }
    )
    // this.gamesList = result.data
    return {
      gamesList: result.data
    }
},  
data() {
  return {
    gamesList: []
  }
},
methods:{
  isPlatformWindows(platform){
    if (platform.includes("Windows")){
      return true
    }
    return false
  }
}
}
</script>

<style lang="scss" scoped>
  .thumbnail {
    max-width: 100%;
  }
  .svg {
    max-width: 20px;    
  }
@media (min-width: 960px){
.container { 
    max-width: 900px;
}
}
</style>