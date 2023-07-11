<template>
  <div class="board">
    <h1>Лента сообщений</h1>
    <message v-for="message in mockData.slice(0, messageNow)" :key="message.authorName + Math.random()"
      :message-data="message">

    </message>
  </div>
</template>

<script>
import mockData from '@/mock-data/feed.json'
import message from '@/components/OneMessage.vue'
export default {
  name: 'MessagesBoard',
  components: {
    message
  },
  data() {
    return {
      mockData: mockData,
      messageNow: 10,
    }
  },
  created() {
    this.testRest()
  },
  methods: {
    moreMessageNow() {
      this.messageNow += 10
    },
    testRest() {
      const interval = setInterval(() => {
        try {
          this.moreMessageNow()
          if (mockData.length <= this.messageNow) {
            clearInterval(interval);
          }
        }
        catch (err) {
          console.log(err);
        }
      }, 4000)

    }
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
