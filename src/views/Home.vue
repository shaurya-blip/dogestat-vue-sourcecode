<template>
  <div class="home">
    <div class="container" @click="showProvider()">

      <h1 class="price" :style="{color:color_in_string}">{{ price }}</h1>

    </div>
  </div>
</template>

<style>
.home{
  position: absolute;
    top: 50%;
    left: 50%;
    -moz-transform: translateX(-50%) translateY(-50%);
    -webkit-transform: translateX(-50%) translateY(-50%);
    transform: translateX(-50%) translateY(-50%);
}

.container{
  padding:200px;
  text-align:center;
  font-family: 'Lato', sans-serif;
}

.green{
  color:green;
}

.red{
  color:red;
}

.price{
  font-size:300px;
}

</style>

<script>
import axios from 'axios'
// @ is an alias to /src

export default {
  name: "Home",
  data(){
    return{
      price:'Loading...', 
      color_in_string:'black'
    }
  },
  methods:{
    callAPI(){
      setInterval(() => {
        axios.get('https://dogeprice-api.herokuapp.com/')
        .then((response) => {
          this.price = response.data['price']
          this.provider = response.data['provider']
          this.color_in_string = response.data['color_in_string']
        });
        // console.clear()
      }, 1000); 
    },
    showProvider(){
      alert(this.provider)
    }
  },
  created() {
    this.callAPI()
  }
};
</script>
