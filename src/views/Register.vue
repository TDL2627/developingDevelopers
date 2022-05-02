<template>
  <div id="register">
      
       <div v-if="loading" >
 <div class="half-circle-spinner">
  <div class="circle circle-1"></div>
  <div class="circle circle-2"></div>
</div>
</div>
  <h1 class="heading animate__slow animate__animated animate__jackInTheBox">REGISTER</h1>
  <form  @submit.prevent="register">
 
<h3>What type of developer are you?</h3>
<input v-model="type" class="putting" placeholder="Type here..." type="text" required>
 <h3>FULL NAME</h3>
<input v-model="fullname" class="putting" placeholder="Type here..." type="text" required>
 <h3>GIT HUB</h3>
<input v-model="github" class="putting" placeholder="Type here..." type="text" required>
 <h3>portfolio</h3>
<input v-model="portfolio" class="putting" placeholder="Type here..." type="text" required>
 <h3>LinkedIN</h3>
<input v-model="linkedin" class="putting" placeholder="Type here..." type="text">
 <h3>Profile Photo</h3>
 <a href="https://imgbb.com/" target="_blank">Upload image and copy image address here</a> <br>
<input v-model="avatar" class="putting" placeholder="Type here..." type="text">
 <h3>EMAIL</h3>
<input v-model="email" class="putting" placeholder="Type here..." type="email" required>
 <h3>PASSWORD</h3>
<input v-model="password" class="putting" placeholder="Type here..." type="password" required>
<br><br>
      <button class="butt subby" type="submit">SUBMIT</button>
  </form>
  <p>Already registered? <router-link to="/login"> Click here</router-link></p>
</div>
</template>

<script>
export default {
data(){
    return{
      
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
 methods: {

   async register() {
     this.loading = true
     try{
    fetch('https://dev2627.herokuapp.com/developers', {
  method: 'POST',
  body: JSON.stringify({
    email:this.email,
    password:this.password,
    fullname:this.fullname,
    linkedin:this.linkedin,
     github:this.github,
    portfolio:this.portfolio,
    type:this.type,
    avatar:this.avatar
  }),
  headers: {
    'Content-type': 'application/json; charset=UTF-8',
  },
})
  .then((response) => response.json())
        .then((user) => {
             localStorage.setItem("jwt", user.jwt);
               localStorage.setItem("id", user.developer._id);
               localStorage.setItem("fullname", user.developer.fullname);
               localStorage.setItem("email", user.developer.email);
                localStorage.setItem("linkedin", user.developer.linkedin);
               localStorage.setItem("type", user.developer.type);
                localStorage.setItem("github", user.developer.github);
                 localStorage.setItem("avatar", user.developer.avatar);
                localStorage.setItem("portfolio", user.developer.portfolio);
               localStorage.setItem("password", user.developer.password);
          this.loading = false
          this.$router.push({ name: "Developers" });
     })
     }
      catch(err)  {
          alert(err);
          this.loading = false
        }
    }
  },
}
</script>

<style scoped>

</style>