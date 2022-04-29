<template>
  <div id="developers">
            <form @submit.prevent="createDeveloper">
        <ul>
          <li>FULL NAME :</li>
          <li> <input v-model="fullname" required type="text"></li>
          <li>BODY</li>
          <li><textarea v-model="body" required type="text" cols="30" rows="10"></textarea></li>
       </ul>


        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
          <button type="submit" class="btn btn-success">Save changes</button>
        </div>
       </form>
  </div>
</template>

<script>
export default {
data(){
    return{
        developers:[],
        fullname:"",
        email:"",
        number:"",
        portfolio:"",
        github:""
    }
},
methods:{
   createDeveloper() {
      fetch("https://mymentor-server.herokuapp.com/note", {
        method: "POST",
        body: JSON.stringify({
          title: this.title,
          body: this.body
    
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
    
        .then((json) => {
          this.loading = false;
          this.title="";
          this.body="";
          alert("Note added");
          this.$router.go()
        })
        .catch((err) => {
          console.log(err)
          alert("It failed.Try again please");
          this.loading = false;
        });
    }
}
}
</script>

<style>

</style>