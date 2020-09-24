<template>
  <div>
    <h1>{{ data.title }}</h1>
    <img class="img-comic" :src=data.img />
    <div class="evaluate">
      <div class="check" id="check_1"  @click="evaluate(1)"></div>
      <div class="check" id="check_2" @click="evaluate(2)"></div>
      <div class="check" id="check_3" @click="evaluate(3)"></div>
      <div class="check" id="check_4" @click="evaluate(4)"></div>
      <div class="check" id="check_5" @click="evaluate(5)"></div>
    </div>
    <span class="score">{{ score }}</span>
  </div>
</template>

<script>

import axios from 'axios';

export default {
  name: 'HelloWorld',
  data () {
    return {
      data: [],
      score: 0
    }
  },
  methods:{
    getComic(){

      //Uso una URL Proxy por problemas relacionados con los CORS
      const PROXY_URL = 'https://cors-anywhere.herokuapp.com/';
      const URL       = 'https://xkcd.com/info.0.json';

      axios.get(PROXY_URL+URL)
      .then(response => {
        this.data = response.data
      })
      .catch(e => console.log(e));
    },
    evaluate(value){
      document.querySelectorAll(".check.evaluated").forEach(obj=>obj.classList.remove("evaluated"));

      for(var i = 1; i <= value; i++){
        document.getElementById('check_'+i).classList.add("evaluated");
      }

      this.score = value;
    }
  },
  mounted() {
    this.getComic();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1, h2 {
    font-weight: normal;
  }

  img{
    margin-bottom: 20px;
  }

  .evaluate{
    width: 100%;
  }

  .check{
    display : inline-block;
    width: 30px;
    height: 30px;
    border: 1px solid black;
    margin: 0 auto;
    border-radius: 50px;
  }

  .evaluated{
    background-color: orangered;
  }

  .score{
    font-size: 20px;
    font-weight: bold;
  }

  .img-comic{
    width: 400px;
    height: 400px;
  }
</style>
