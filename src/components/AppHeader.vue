<template>
  <nav>
    <ul id="menu">
      <li><router-link to="/"><img src="/static/images/foodicon.png"/></router-link></li>
      <li><form v-on:submit.prevent="search">
	<input v-model="keywords" placeholder="Search">
	<a href="#" v-on:click="search" class="search"><i class="fas fa-search"></i></a>
      </form></li>
      <li class="right" v-if="loggedIn">
	<router-link :to="{ name: 'UserPage', params: {userID: user.id}}">{{user.username}}</router-link> <button  class="primary" @click="logout" href="#">Logout</button></p>
      </li>
      <li class="right" v-else>
	<form v-on:submit.prevent="login">
	  <input v-model="email" placeholder="Email">
	  <input v-model="password" type="password" placeholder="Password">
	  <button class="primary" type="submit">Login</button>
    <p v-if="loginError" class="flexRight error">{{loginError}}</p>
	</form>
      </li>
    </ul>
    <!-- <div class="flexWrapper errorPlace">
      <p v-if="loginError" class="flexRight error">{{loginError}}</p>
    </div> -->
  </nav>
</template>

<script>
 export default {
   name: 'AppHeader',
   data () {
     return {
       keywords: '',
       email: '',
       password: '',
     }
   },
   computed: {
     user: function() {
       return this.$store.getters.user;
     },
     loggedIn: function() {
       return this.$store.getters.loggedIn;
     },
     loginError: function() {
       return this.$store.getters.loginError;
     },
     numberFollowing: function() {
       return this.$store.getters.following.length;
     },
     numberFollowers: function() {
       return this.$store.getters.followers.length;
     }
   },
   methods: {
     search: function() {
       this.$router.push({ path: '/search', query: { keywords: this.keywords }})
       this.keywords = '';
     },
     login: function() {
       this.$store.dispatch('login',{
         email: this.email,
         password: this.password,
       }).then(user => {
	 this.email = '';
	 this.password = '';
       });
     },
     logout: function() {
       this.$store.dispatch('logout');
     }
   }
 }
</script>

<style scoped>
 /* Strip the ul of padding and list styling */
 nav {
     display: grid;
     /*margin-bottom: 8vw;*/
     height: 20vw;
 }
 ul {
     list-style-type:none;
     margin:0;
     padding:0;
     text-decoration: none;
     text-align: center;
     vertical-align: middle;
 }
 /* Create a horizontal list with spacing */
 li {
     vertical-align: middle;
     display:inline-block;
     float: left;
     margin-right: 1vw;
     height: 14vw;
     text-align: center;
     line-height: 14vw;
     color: #666;
     text-decoration: none;
 }
 /*Active color*/
 li a.active {
 }
 /*Hover state for top level links*/
 li:hover a {
 }
 input {
     height: 1vw;
     width: 7vw;
     font-size: calc(8px + 0.5vw);
 }
 .search {
     margin-left: 1vw;
 }
 .right {
     float: right;
 }
 .errorPlace {
     height: 20px;
 }
 img {
     width: calc(30px + 6vw);
     padding: 2vw;
 }
 button {
  font-size: calc(8px + 0.5vw);
  width: calc(20px + 5vw);
  }
</style>
