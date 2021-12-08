<template>
  <p v-if="messages.length === 0">Waiting for messages...</p>
  <ul v-else>
    <li v-for="(message, index) in reversedMessages" :key="index">
      {{ message }}
    </li>
  </ul>
</template>

<script>
import { ref, computed } from 'vue'
import useEventBus from '../composables/useEventBus'

export default {
  name: 'MessagesList',
  setup() {
    const { onEvent } = useEventBus()
    const messages = ref([])
    const reversedMessages = computed(() => messages.value.slice().reverse())

    onEvent('message', (payload) => {
      console.log('message:', payload)
      messages.value.push(payload)
    })

    onEvent('clear-messages', () => {
      console.log('clear-messages')
      messages.value.length = 0
    })

    return {
      onEvent,
      messages,
      reversedMessages
    }
  }
}
</script>
