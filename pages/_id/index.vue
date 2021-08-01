<template>
 <v-app>
   <v-container>
     <v-row>
       <v-col cols="4">
         <img :src="game.thumbnail" alt="">
       </v-col>
       <v-col cols="8">
         <h1>{{ game.title }}</h1>
         <p>{{ game.description }}</p>
         <v-row>
         <v-col v-for="screenshot in game.screenshots" :key="screenshot.id">
           <img :src="screenshot.image" alt="" class="screenshot">
         </v-col>
         </v-row>
       </v-col>

     </v-row>
   </v-container>
 </v-app>
</template>

<script>
  export default {
    async asyncData({ $axios, params }) {
    const config = {
      "x-rapidapi-key": "bf42eb820cmsh1b4e9fb2ae3fe7dp1893f1jsn4d6ab01716e3",
      "x-rapidapi-host": "free-to-play-games-database.p.rapidapi.com"
    }
  const result = await $axios.get(
    "https://free-to-play-games-database.p.rapidapi.com/api/game",
    {
      params: {id: params.id },
      headers: config
    }
    )
    // this.gamesList = result.data
    return {
      game: result.data
    }
},  
    
  }
</script>

<style lang="scss" scoped>
  .screenshot{
    height: 250px;
    width: 100%;
    object-fit: cover;
  }
</style>