<template>
  <div>
    <h3>{{tweet.user.name}}</h3>
    <p>{{tweet.text}}</p>
  </div>
</template>

<script>
import { defineComponent  } from 'vue'

export default defineComponent({
  props: {
    tweet: {
      type: Object,
      required: true
    },
  },
})
</script>