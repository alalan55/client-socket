<template>
  <div class="message">
    <div class="message-content">
      <div class="content-input">
        <input
          type="text"
          placeholder="Digite sua mensagem"
          v-model="message"
          @keyup.enter="sendMessage"
        />
      </div>

      <div class="content-action">
        <button @click="sendMessage">Enviar</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  setup(props, { emit }) {
    const message = ref("");
    const sendMessage = () => {
      emit("sendMessage", message.value);
      message.value = "";
    };
    return {
      message,
      sendMessage,
    };
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/scss/variables.scss";
.message {
  width: 100%;
  height: 100%;
  padding: $p-1 0;

  .message-content {
    background: white;
    border-radius: 10px;
    height: 100%;
    width: 100%;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: 1fr;

    grid-template-areas: "input input input action";

    .content-input {
      grid-area: input;
      input {
        width: 100%;
        height: 100%;
        padding: 1rem;
        background: none;
        border: none;

        &:focus {
          outline: none;
        }
      }
    }
    .content-action {
      grid-area: action;
      display: flex;
      align-items: center;
      justify-content: flex-end;
      padding: 0 0.8rem 0 0.5rem;

      button {
        padding: 1rem 0.5rem;
        border-radius: 10px;
        border: none;
        background: $blue-1;
        color: white;
        font-weight: 500;
        width: 150px;
        cursor: pointer;
        transition: 0.2s ease-in-out;

        &:hover {
          background: $blue-2;
        }

        @media (max-width: $mobile) {
          width: 100%;
          padding: 0.8em 0.5rem;
        }

        @media (min-width: $x-large) {
          font-size: 1.1em;
          font-weight: 600;
          height: 60%;
          padding: 0.8rem 1.5rem;
        }
      }
    }

    & > div {
      // border: 1px solid blue;
    }
  }
}
</style>
