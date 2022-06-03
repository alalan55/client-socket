<template>
  <div class="message">
    <div class="message-content">
      <div class="content-input">
        <input type="text" placeholder="Digite sua mensagem" />
      </div>

      <div class="content-action">
        <button>Enviar</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  setup() {
    return {};
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/scss/variables.scss";
.message {
  //   background: red;
  width: 100%;
  height: 100%;
  padding: $p-1;

  .message-content {
    border: 1px solid;
    height: 100%;
    width: 100%;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: 1fr;

    grid-template-areas: "input input input action";

    .content-input {
      grid-area: input;
    }
    .content-action {
      grid-area: action;
    }

    & > div {
      border: 1px solid blue;
    }
  }
}
</style>