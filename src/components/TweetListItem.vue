<template>
  <li :class="popularTweetsClass"><span>ID:{{tweet.id}}
    </span><img :src="tweet.img"><span> {{tweet.name}}{{tweet.handle}}</span>
   <p>{{ tweet.tweet }}</p>
   <span>Likes: {{tweet.likes}}</span></li>
</template>

<script>
export default {
    name: 'tweet-list',
    props:['tweet'],
    computed: {
        popularTweetsClass: function() {
            return this.tweet.likes>10 ? 'popular':'';
        }
    }
}
</script>

<style>
li{
    list-style: none;
    border-style:groove;
    padding:10px;
    margin: 10px;
}
.popular {
    border-color:orangered;
    border-width: 5px;
    border-style: ridge;
}

img {
    width:10%;
}
</style>