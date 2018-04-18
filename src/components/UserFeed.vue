<template>
  <div class="feed">
    <div>
      <form enctype="multipart/form-data" v-on:submit.prevent="tweet" class="tweetForm">
        <h1>Share a Recipe</h1>
	       <textarea v-model="text" placeholder="Be sure to include your recipe's name, all needed igredients, and instructions on how to make it."/>
	<div v-bind:style="{inactive: !imagePreview, active:imagePreview }">
	  <img class="preview" v-bind:src="imageData">
	</div>
	<div class="buttons">
	  <div class="icon">
	   <!--  <label for="file-input">
	      <i class="far fa-image" aria-hidden="true"></i>
	    </label> -->
	    <input id="file-input" type="file" v-on:change="previewImage" accept="image/*" class="input-file">
	  </div>
	  <div class="buttonWrap">
	    <button class="alternate" type="submit">Share Recipe!</button>
	  </div>
	</div>
      </form>
    </div>
    <feed-list class="feedlist" v-bind:feed="feed" />
  </div>
</template>

<script>
 import FeedList from './FeedList';
 export default {
   name: 'UserFeed',
   data () {
     return {
       text: '',
       imageData: '',
       imagePreview: false,
       file: '',
     }
   },
   components: { FeedList },
   computed: {
     feed: function() {
       return this.$store.getters.feed;
     },
   },
   created: function() {
     this.$store.dispatch('getFeed');
   },
   methods: {
     tweet: function() {
       this.$store.dispatch('addTweet',{
         tweet: this.text,
	 image: this.file,
       }).then(tweet => {
	 this.text = "";
	 this.imageData = "";
	 this.imagePreview = false;
       });
     },
     previewImage: function(event) {
       const input = event.target;
       // Ensure that you have a file before attempting to read it
       if (input.files && input.files[0]) {
	 this.file = input.files[0];
         // create a new FileReader to read this image and convert to base64 format
         const reader = new FileReader();
         // Define a callback function to run, when FileReader finishes its job
         reader.onload = (e) => {
           // Read image as base64 and set to imageData
           this.imageData = e.target.result;
	   this.imagePreview = true;
         }
         // Start the reader job - read file as a data url (base64 format)
         reader.readAsDataURL(input.files[0]);
       }
     }
   }
 }
</script>

<style scoped>
 .feedlist {
    margin-left: 3vw;
 }
 .tweetForm {
     background: #eee;
     padding: 10px;
     margin-bottom: 10px;
     margin-left: 3vw;
    background-image: url("/static/images/food.jpg");
 }
 .buttons {
     display: flex;
     justify-content: space-between;
 }
 .icon {
     font-size: 2em;
     padding: 0px;
 }
 .icon:active {
     transform: translateY(4px);
 }
 .buttonWrap {
     width: 20%;
 }
 button {
     height: 2em;
     font-size: 0.9em;
     float:right;
 }
 textarea {
     width: 98%;
     height: 8em;
     padding: 2px;
     margin: 1vw;
     resize: none;
     box-sizing: border-box;
     padding: 1vw;
    font-size: 3vw;
    font-weight: normal;
    opacity: 0.9;
}
 h1 {
    margin-bottom: 0px;
    align-content: center;
    text-align: center;
    color: white;
    padding: 2vw 3vw 2vw 3vw;
    text-shadow: 0.2vw 0.2vw 0.4vw black;
    font-family: 'Poiret One', cursive;
 }
 p {
  padding: 1vw;
  color: white;
  text-shadow: 0.2vw 0.2vw 0.4vw black;
  font-size: 4vw;
 }
 input[type="file"] {
     display: none;
 }
 .imagePreview {
     padding: 0px;
     height: 150px;
 }
 active {
     display: block;
 }
 inactive {
     display: none;
 }
 img {
     max-width: 100%;
     max-height: 100%;
 }
</style>
