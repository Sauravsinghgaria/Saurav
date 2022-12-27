<template>
  <div class="container">
    <div v-for="i in listBears" class="flip-card">
      <div class="flip-card-inner">
        <div class="flip-card-front">
          <img :src=i.image_url style="height: 175px; width: 250px" alt="image">
          <h1>{{i.name}}</h1>
        </div>
        <div class="flip-card-back">
          <h3> {{i.tagline}} </h3>
          <p>{{i.description}}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      listBears:null
    }
  },
  mounted(){
    fetch("https://api.punkapi.com/v2/beers")
      .then(res => res.json())
      .then(data => this.listBears = data)
      .catch(err => console.log(err.message))
  }
}
</script>

<style>
.container{
  margin: auto;
}
.flip-card {
  float: left;
  margin: 10px;
  background-color: transparent;
  width: 300px;
  height: 300px;
  perspective: 1000px; /* Remove this if you don't want the 3D effect */
}

/* This container is needed to position the front and back side */
.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  box-shadow: 0 4px 8px rgba(0,0,0,0.4);
  transform-style: preserve-3d;
}

/* Do an horizontal flip when you move the mouse over the flip box container */
.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

/* Position the front and back side */
.flip-card-front, .flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden; /* Safari */
  backface-visibility: hidden;
}

/* Style the front side (fallback if image is missing) */
.flip-card-front {
  background-color: #ffffff;
  color: BLACK;
}

/* Style the back side */
.flip-card-back {
  background-color: #FCF6F5FF;
  color: BLACK;
  transform: rotateY(180deg);
}

</style>
