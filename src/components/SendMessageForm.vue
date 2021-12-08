<template>
  <form class="row g-3" @submit.prevent="onSubmit">
    <div class="col">
      <input
        type="text"
        class="form-control"
        placeholder="Enter your message"
        v-model="message"
        autofocus
      />
    </div>
    <div class="col-auto">
      <button type="submit" class="btn btn-primary">Send</button>
    </div>
  </form>
</template>

<script>
import { ref } from 'vue'
import useEventBus from '../composables/useEventBus'

export default {
  name: 'SendMessageForm',
  setup() {
    const { emitEvent } = useEventBus()
    const message = ref('')

    return {
      message,
      onSubmit() {
        emitEvent('message', message.value || 'Empty message..')
        message.value = ''
      }
    }
  }
}
</script>
