<template>
  <div>
    <h1>Tweet List</h1>
    <h2>Total Likes: {{totalLikes}}</h2>
    <form v-on:submit.prevent="saveTweet">
      <h3>Add a Tweet</h3>
      <label for="name">Name:</label>
      <input id="name" type="text" v-model="newTweet.name" />
      <label for="handle">Handle:</label>
      <input id="handle" type="text" v-model="newTweet.handle" />
      <label for="tweet">Tweet:</label>
      <input id="tweet" type="text" v-model="newTweet.tweet" />
      <label for="likes">Likes:</label>
      <input id="likes" type="number" v-model.number="newTweet.likes" />
      <input type="submit" value="Add Tweet"/>
    </form>
    <div id = "filterTweets">
      <h3>Filter by Likes</h3>
      <input type="number" v-model.number="filterTweets">
    </div>
    <ul>
      <tweet-list v-for="(tweet, index) in filteredTweets" :key="index" :tweet="tweet"></tweet-list>
    </ul>
  </div>
</template>

<script>
import TweetListItem from './components/TweetListItem.vue';

export default {
  name: 'app',
  data() {
  return {
    tweets:[
      {
        id: 1,
        name: 'James',
        handle: '@jokerjames',
        img: 'https://semantic-ui.com/images/avatar2/large/matthew.png',
        tweet: "If you don't succeed, dust yourself off and try again.",
        likes: 10,
      },
      {
        id: 2,
        name: 'Fatima',
        handle: '@fantasticfatima',
        img: 'https://semantic-ui.com/images/avatar2/large/molly.png',
        tweet: 'Better late than never but never late is better.',
        likes: 12,
      },
      {
        id: 3,
        name: 'Xin',
        handle: '@xeroxin',
        img: 'https://semantic-ui.com/images/avatar2/large/elyse.png',
        tweet: 'Beauty in the struggle, ugliness in the success.',
        likes: 18,
      }
    ],
    newTweet: {
      id:0,
      name:"",
      handle:"",
      img: 'https://semantic-ui.com/images/avatar2/large/molly.png',
      tweet: "",
      likes:0,
    },
    filterTweets:0
  }
},
  computed:{
          totalLikes: function(){
              return this.tweets.filter(tweet => tweet.likes >= this.filterTweets).reduce((total, tweet) => total + tweet.likes,0);
          },
          filteredTweets: function(filterTweets) {
            return this.tweets.filter(tweet => tweet.likes >= this.filterTweets);
          }
      },
  components:{
        'tweet-list':TweetListItem
  },
  methods: {
    saveTweet: function() {
      this.tweets.unshift(this.newTweet);
      this.newTweet.id=this.tweets.reduce(function(prev,curr) {
        return prev.id < curr.id ? prev.id : curr.id;}) + 1;

      this.newTweet = {
        name:"",
        handle:"",
        tweet:"",
        likes:0,
      }
    }
  }
}
</script>

<style>
body {
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  margin:20px;
}
input{
  margin: 10px;
}
</style>