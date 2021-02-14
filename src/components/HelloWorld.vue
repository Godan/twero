<template>
  <div class="hello" v-if="tweet">
    <tweet-card :tweet="tweet" />
  </div>
</template>

<script>
import electron from 'electron';
import tweetCard from './tweet'
let params = {q: "#この想い赤にのせて", result_type: "recent"}

export default {
  name: 'HelloWorld',
    components: {
      tweetCard
  },
  props: {
    msg: String
  },
  data() {
    return {
      twitterClient: null,
      tweetDisplay: null,
      tweets: [],
      tweet: undefined
    }
  },
  created () {
    this.twitterClient = setInterval(async() => {
      const data = await electron.ipcRenderer.invoke("btnExecInvoke_onclick", params);
      console.log(data)
      if(data.search_metadata.max_id){
        params['since_id'] = data.search_metadata.max_id
      }
      this.tweets = data.statuses.slice(1)
      console.log(this.tweets)
      this.tweet = this.tweets.pop()
      console.log(this.tweet.text)
    }, 10000)
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
