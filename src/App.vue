<script>
import { createApp } from 'vue'

export default {
  data() {
    return {
      message: 'САлам Вью '
    }
  },
  methods: {
    reverseMessage() {
      this.message = this.message
        .split('')
        .reverse()
        .join('')
    }
  }
}

</script>

<template>
  <div id="reverse">
    <p>{{ message }}</p>
    <button v-on:click="reverseMessage">press me to reverse</button>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  overflow: hidden;
}
.greeting {
  color: rebeccapurple;
  font-weight: bold;
}

#reverse {
  height: 100vh;
  width: 100wh;
  background-color: aqua;
}
</style>
