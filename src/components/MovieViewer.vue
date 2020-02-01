<template>
<div>
  <b-card-group columns>
    <b-card
     v-for="item in items"
     :key="item.id"
     :img-src="item.images.fixed_width.url"
     :img-alt="item.title"
     >
     <b-card-text>
       <a :href="gif.url" target="_blank"> {{item.title}}</a>
     </b-card-text>
    </b-card>
  </b-card-group>
</div>
</template>

<script>
/* eslint-disable no-console */
import axios from 'axios';

const TMDB_URL = "https://api.themoviedb.org/3"
const API_KEY = "8c988e866c6227c3a7cc9b31868699bb"

export default {
  name: "MovieViewer",
  components:{

  },
  data(){
    return{
      items:[],
      term:''
    };
  },
  mounted() {
   axios.get(`${TMDB_URL}/movie/popular?api_key=${API_KEY}`)
        .then(response => {
          this.items = response.data.data
        })
        .catch(error => console.log(error));
  },
  methods:{
   getMovies(){
     let app = this;
           let token = localStorage.getItem('token');
           axios.get('/movie/latest', {
             headers: { Authorization: "Bearer " + token}
           })
           .then(function(response){
             console.log(response);
            app.items = response.data.data;
          })
           .catch(function(error){
             console.log(error);
           })
      }
  }
};
</script>

<style>
.seach-box{
  margin-top: 20px;
  margin-bottom: 20px;
}
</style>
