<template>
  <div class="container py-4 col-md-8">
    <header class="pb-3 border-bottom mb-4">
      <h1 class="fs-3">Demo: Vue Event Bus using the Composition API</h1>
      <span class="fs-6">owre.se - Pontus Öwre</span>
    </header>
    <div class="p-5 bg-light mb-4">
      <div class="container-fluid py-3">
        <p class="fs-4">
          The purpose of this demo is to demonstrate how to leverage the
          Composition API to add and use an event bus in your vue project
        </p>
        <div class="row gx-3">
          <div class="col-auto">
            <a
              href="https://owre.se/vue-3-event-bus-using-the-composition-api/"
              class="btn btn-primary col-auto"
            >
              Read the article
            </a>
          </div>
          <div class="col-auto">
            <a
              href="https://github.com/owre/demo-vue-3-event-bus-using-the-composition-api"
              class="btn btn-outline-primary col"
            >
              Browse the source
            </a>
          </div>
        </div>
      </div>
    </div>
    <send-message-form class="mb-4" />
    <button
      class="btn btn-secondary w-100 mb-4"
      @click="shouldShowMessages = !shouldShowMessages"
    >
      {{ shouldShowMessages ? 'Unmount' : 'Mount' }} messages container
    </button>
    <div class="p-5 text-white bg-dark rounded-3" v-if="shouldShowMessages">
      <div class="row g-3">
        <h2 class="col">Messages</h2>
        <button
          class="btn btn-sm btn-secondary col-auto"
          @click="clearMessages"
        >
          Clear messages
        </button>
      </div>
      <hr />
      <messages-list />
    </div>
    <p v-else class="text-center">
      Check the console to see that the MessageList component is not logging any
      more messages. Event handlers have been successfully removed.
    </p>
  </div>
</template>

<script>
import { ref } from 'vue'
import SendMessageForm from './components/SendMessageForm.vue'
import MessagesList from './components/MessagesList.vue'
import useEventBus from './composables/useEventBus'

export default {
  name: 'App',
  components: {
    SendMessageForm,
    MessagesList
  },

  setup() {
    const { emitEvent } = useEventBus()
    const shouldShowMessages = ref(true)

    return {
      shouldShowMessages,
      clearMessages() {
        emitEvent('clear-messages')
      }
    }
  }
}
</script>
