<template>
  <div class="client-template">
    <div class="view-area">
      <View />
    </div>
    <div class="message-area">
      <Message />
    </div>
  </div>
</template>

<script setup>
import View from "@/components/organisms/ViewFinder.vue";
import Message from "@/components/organisms/MessageEntry.vue";
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

  .view-area {
    grid-area: visor;
  }
  .message-are {
    grid-area: message;
  }

  & > div {
    border-radius: 10px;
    overflow: hidden;
    border: 1px solid;
  }
}
</style>