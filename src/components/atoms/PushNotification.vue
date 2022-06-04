<template>
  <div class="notification">
    <div class="content-notification">
      <div class="push-message" :class="stylePush">
        <span>{{ message }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    message: { type: String, required: true, default: "Insira uma mensagem" },
    stylePush: { type: String, required: true, default: "success" },
  },
  setup() {
    return {};
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/scss/variables.scss";
.notification {
  position: fixed;
  height: 100vh;
  width: 100vw;
  top: 0;
  left: 0;
  padding: 0 $p-1;

  .content-notification {
    height: 25vh;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    .push-message {
      border-radius: 4px;
      padding: 0.9rem;
      display: inline-block;
      min-width: 20vw;
      text-align: center;
      position: relative;

      span {
        color: white;
        font-weight: 500;
      }
    }

    .success {
      background: $green-1;
    }
    .error {
      background: $red-1;
    }
  }
}
</style>