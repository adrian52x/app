<template>
  <div class="circle">
    <img v-bind:src="imgPath">
  </div>
  
 
</template>

<script>


export default {
  name: 'PokemonImage',
  props: {
    imgPath: String
  },
  methods: {
    
  }
  
}
</script>


<style scoped>

img {
    height: 150px;
    width: 150px;
    border-radius: 80%;
    
}
.circle{
    height: 150px;
    width: 150px;
    background: rgb(255, 255, 255);
    border-radius: 50%;
}

</style>
