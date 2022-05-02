<template>
  <div id="developers">

 <div v-if="loading" >
 <div class="half-circle-spinner">
  <div class="circle circle-1"></div>
  <div class="circle circle-2"></div>
</div>
</div>

<div class="container">
  <div class="row"  v-for="developer in developers" :key="developer.email">
    <div class="col-lg-4">
     <h3>{{developer.fullname}}</h3>
     <h5>{{developer.type}}</h5>
     <p>{{developer.email}}</p>
     <a target="_blank" :href="developer.github">GIT HUB</a> |
     <a target="_blank" :href="developer.portfolio">PORTFOLIO</a> |
     <a target="_blank" :href="developer.linkedin">LINKEDIN</a> 
   <img class="pp" :src="developer.avatar">
    </div>
  
    <hr>
  </div>
</div>


        
  </div>
</template>

<script>
export default {
data(){
    return{
        developers:[],
        fullname:"",
        email:"",
        linkedin:"",
        avatar:"",
        password:"",
        type:"",
        portfolio:"",
        github:"",
          loading:false
    }
},


  
async created () {
    this.loading = true
    try {
      const res = await fetch('https://dev2627.herokuapp.com/developers')
      this.developers = await res.json()
      this.loading = false
    } catch (error) {
      console.log(error)
      this.loading = false
    }
  }

}
</script>

<style scoped>
.pp{
  height: 200px;
}
/* loader */
.half-circle-spinner, .half-circle-spinner * {
      box-sizing: border-box;
    }

    .half-circle-spinner {
      width: 60px;
      height: 60px;
      border-radius: 100%;
     position: fixed;
      top:45%;
      left: 50%;
    }

    .half-circle-spinner .circle {
      content: "";
      position: absolute;
      width: 100%;
      height: 100%;
      border-radius: 100%;
      border: calc(60px / 10) solid transparent;
    }

    .half-circle-spinner .circle.circle-1 {
      border-top-color: white;
      animation: half-circle-spinner-animation 1s infinite;
    }

    .half-circle-spinner .circle.circle-2 {
      border-bottom-color: #1d92ff;
      animation: half-circle-spinner-animation 1s infinite alternate;
    }

    @keyframes half-circle-spinner-animation {
      0% {
        transform: rotate(0deg);

      }
      100%{
        transform: rotate(360deg);
      }
    }
</style>