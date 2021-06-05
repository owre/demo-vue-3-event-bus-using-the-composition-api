# Demo: Vue Event Bus using the Composition API

The purpose of this demo is to demonstrate how to leverage the Composition API to add and use an event bus in your vue project

[Read the article](https://owre.se/vue-3-event-bus-using-the-composition-api/)

### src/components/MessagesList.vue

Component that lists messages that it receives from the event bus. It will clear messages from the list when it receives the 'clear-messages' event.

### src/components/SendMessageForm.vue

Component that is responsible to emit the "message" event which the MessagesList component consumes.


### src/composables/useEventBus.js

Holds the "core" logic. It utilizes tiny-emitter to emit and subscribe to events.
