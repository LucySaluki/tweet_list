<template>
  <li><img :src="tweet.img"><span> {{tweet.name}}{{tweet.handle}}</span>
   <p>{{ tweet.tweet }}</p>
   <span>Likes: {{tweet.likes}}</span></li>
</template>

<script>
export default {
    name: 'tweet-list',
    props:['tweet'],
}
</script>

<style>
li{
    list-style: none;
    border-style:groove;
    padding: 10px;
    margin: 10px;
}
img {
    width:10%;
}
</style>