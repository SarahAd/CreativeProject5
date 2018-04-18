<template>
  <div class="column">
    <div class="welcome">
      <h1>Red Plate</h1>
      <img src="/static/images/foodicon.png" alt="Icon">
      <h2>Find recipes.  Follow friends.  Share your favorite foods.</h2>
    </div>

    <div class="register">
      <form v-on:submit.prevent="register">
        <p>1. Choose a user name (this is how you will be known by others on Red Plate)</p>
        <input class="name" v-model="username" placeholder="User Name">
        <p>2. Create an account</p>
        <input class="name" v-model="name" placeholder="First and Last Name"><br/>
        <input class="email" v-model="email" placeholder="Email Address">
        <input class="password" type="password" v-model="password" placeholder="Password"><br/>
        <button class="alternate" type="submit">Register</button>
      </form>
    </div>
      <p class="error">{{registerError}}</p>
    <div class='footer'>
      <a href="https://github.com/SarahAd/CreativeProject5">Find My Code On GitHub!</a>
    </div>
  </div>
  </div>
  <!--  <div class='footer'>
      <a href="https://github.com/SarahAd/CreativeProject3"><img src="/static/images/githublogo.png"></a>
      <a href="https://github.com/SarahAd/CreativeProject3">Find My Code On GitHub!</a>
   </div> -->

</template>

<script>
 export default {
   name: 'WelcomePage',
   data () {
     return {
       username: '',
       email: '',
       password: '',
       name: '',
     }
   },
   computed: {
     registerError: function() {
       return this.$store.getters.registerError;
     },
   },
   methods: {
     register: function() {
       this.$store.dispatch('register',{
	 username: this.username,
         email: this.email,
         password: this.password,
	 name: this.name,
       });
     }
   }
 }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.column {
    background-image: url("/static/images/food.jpg");
    margin-left: -2vw;
    width: 101vw;
}
.welcome {
    background-color: rgba(255,255,255,0.9);
    height: 100%;
}
/*.register {
  background-color: rgba(255,255,255,0.3);
}*/
.footer {
    padding: 5vw;
    font-size: 2.5vw;
}
 img {
    width: calc(80px + 20vw);
    margin: auto;
    display: block;
 }

 h1 {
    font-size:calc(30px + 5vw);
 }

 h1, h2 {
    margin-bottom: 0px;
    align-content: center;
    text-align: center;
    color: #E03C31;
    padding: 2vw 4vw 2vw 4vw;
    text-shadow: 0.2vw 0.2vw 0.4vw white;
    font-family: 'Poiret One', cursive;

 }
 p {
    margin-top: 0px;
    font-size: 1.3em;
    font-weight: normal;
    color: white;
    font-weight: bold;
    padding: 2vw 5vw 0vw 6vw;
    text-shadow: 0.2vw 0.2vw 0.4vw black;
 }
 a {
    text-shadow: 0.2vw 0.2vw 0.4vw black;
    font-size: calc(20px + 1vw);
    color: white;
    font-weight: bold;
 }
 .name {
    opacity: 0.9;
    margin: 1vw 0vw 1vw 6vw;
    font-size:calc(8px + 1.5vw);
    border: none;
 }
 .email {
    opacity: 0.9;
    margin: 1vw 1.3vw 1vw 6vw;
    font-size:calc(8px + 1.5vw);
    border: none;
 }
 .password {
    opacity: 0.9;
    margin: 1vw 0vw 1vw 0vw;
    font-size:calc(8px + 1.5vw);
    border: none;
 }
 button {
    margin: 1vw 1vw 5vw 6vw;
 }
 @media only screen and (min-width: 800px) {
  .column {
    display: grid;
    grid-template-columns: 5fr 6fr;
    background-size: 65vw;
  }
  .name {
    width: 40.4vw;
  }
  .email {
    width: 18vw;
  }
  .password {
    width: 18vw;
  }
}
@media only screen and (max-width: 800px) {
  .column {
    display: grid;
    grid-template-columns: 1fr;
    background-size: 130vw;
  }
  .name {
    width: 82vw;
  }
  .email {
    width: 38vw;
  }
  .password {
    width: 38vw;
  }
}

</style>
