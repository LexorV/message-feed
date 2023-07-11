<template>
  <div class="board">
    <h1>{{ msg }}</h1>
    <message v-for="message in mockData"
     :key="message.authorName + Math.random()"
     :message-data="message"
     >

    </message>
  </div>
</template>

<script>
import mockData from '@/mock-data/feed.json'
import message from '@/components/OneMessage.vue'
export default {
  name: 'HelloWorld',
  components: {
    message
  },
  data () {
    return {
      mockData: mockData
    }
  },
  props: {
    msg: String
  },
  mounted () {
    console.log(this.mockData[0])
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.board {
  display: flex;
  flex-direction: column;
  gap: 20px;
  margin: 50px;
}
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
