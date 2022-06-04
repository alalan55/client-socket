<template>
  <div class="client-template">
    <div class="view-area">
      <View :messages="messages" />
    </div>
    <div class="message-area">
      <Message @sendMessage="sendMessage" />
    </div>

    <Teleport to="#modal">
      <PushNotification :message="message" v-if="pushIsOpen" stylePush="success" />
    </Teleport>
  </div>
</template>

<script>
import { ref } from "vue";
import View from "@/components/organisms/ViewFinder.vue";
import Message from "@/components/organisms/MessageEntry.vue";
import PushNotification from "../atoms/PushNotification.vue";

export default {
  components: {
    Message,
    View,
    PushNotification,
  },
  setup() {
    let ws;
    const messages = ref([]);
    const message = ref("");
    const pushIsOpen = ref(false);

    const showMessage = (message) => {
      messages.value.push(message);
    };

    const init = () => {
      if (ws) {
        ws.onerror = ws.onopen = ws.onclose = null;
        ws.close();
      }
      ws = new WebSocket(import.meta.env.VITE_APP_URL);

      ws.onopen = () => {
        message.value = "Conexão aberta!";
        setTimeout(() => {
          pushIsOpen.value = true;
        }, 1500);
        setTimeout(() => {
          pushIsOpen.value = false;
        }, 3500);
      };
      ws.onmessage = ({ data }) => showMessage(data);
      ws.onclose = () => (ws = null);
    };

    const sendMessage = (message) => {
      if (!ws) {
        console.log("Sem conexão com o web socket");
        return;
      }
      ws.send(message);
      showMessage(message);
    };

    init();

    return { messages, sendMessage, message, pushIsOpen };
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/scss/variables.scss";

.client-template {
  height: 100vh;
  background: $yellow-1;
  padding: 2rem;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: repeat(5, 1fr);
  gap: 1rem;
  grid-template-areas:
    "visor"
    "visor"
    "visor"
    "visor"
    "message";
  transition: 0.2s ease-in-out;

  .view-area {
    grid-area: visor;
  }
  .message-are {
    grid-area: message;
  }

  @media (max-width: $mobile) {
    grid-template-rows: repeat(6, 1fr);
    grid-template-areas:
      "visor"
      "visor"
      "visor"
      "visor"
      "visor"
      "message";
  }

  & > div {
    border-radius: 10px;
    overflow: hidden;
    // border: 1px solid;
  }
}
</style>
