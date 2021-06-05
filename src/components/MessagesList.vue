<template>
  <p v-if="messages.length === 0">Waiting for messages...</p>
  <ul v-else>
    <li v-for="(message, index) in reversedMessages" :key="index">{{ message }}</li>
  </ul>
</template>

<script>
import { ref } from 'vue'
import useEventBus from '../composables/useEventBus'

export default {
  name: 'MessagesList',
  setup() {
    const { onEvent } = useEventBus()
    const messages = ref([])

    return {
      onEvent,
      messages
    }
  },
  computed: {
    reversedMessages() {
      return [...this.messages].reverse()
    }
  },
  created() {
    this.onEvent('message', (payload) => {
      console.log('message:', payload)
      this.messages.push(payload)
    })

    this.onEvent('clear-messages', () => {
      console.log('clear-messages')
      this.messages.length = 0
    })
  }
}
</script>
