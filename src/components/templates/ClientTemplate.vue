<template>
  <div class="client-template">
    <div class="view-area">
      <View :messages="messages" />
    </div>
    <div class="message-area">
      <Message @sendMessage="sendMessage" />
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import View from "@/components/organisms/ViewFinder.vue";
import Message from "@/components/organisms/MessageEntry.vue";

export default {
  components: {
    Message,
    View,
  },
  setup() {
    let ws;
    const messages = ref([]);

    const showMessage = (message) => {
      messages.value.push(message);
    };

    const init = () => {
      if (ws) {
        ws.onerror = ws.onopen = ws.onclose = null;
        ws.close;
      }

      //   ws = new WebSocket(import.meta.env.VUE_APP_URL);
      ws = new WebSocket("ws://localhost:6969");

      ws.onopen = () => {
        console.log("Conexão aberta");
      };
      ws.onmessage = ({ data }) => {
        console.log("chegou mensagem aqui manooooo");
        showMessage(data);
      };
      ws.onclose = () => (ws = null);
    };

    const sendMessage = (message) => {
      if (!ws) {
        console.log("Sem conexão com o web socket");
        return;
      } else {
        ws.send(message);
        ws.onmessage = (data) => console.log("data aqui", data);
        showMessage(message);
      }
    };

    init();

    return { messages, sendMessage };
  },
};

//   data() {
//     return {
//       ws: null,
//       messages: [],
//     };
//   },
//   created(){
//       this.init()
//   },
//   methods: {
//     showMessage(message) {
//       this.messages.push(message);
//     },
//     init() {
//       if (this.ws) {
//         this.ws.onerror = this.ws.onopen = this.ws.onclose = null;
//         this.ws.close;
//       }

//       this.ws = new WebSocket("ws://localhost:6969");

//       this.ws.onopen = () =>{
//           console.log('Conexão aberta')
//       }
//       this.ws.onmessage = ({data}) => this.showMessage(data);
//       this.ws.onclose = () => this.ws = null;
//     },
//     sendMessage(message){
//         if(!this.ws){
//             console.log('Sem conexão com a API')
//             return
//         }
//         this.ws.send(message)
//         this.showMessage(message)
//     }
//   },
// };
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
