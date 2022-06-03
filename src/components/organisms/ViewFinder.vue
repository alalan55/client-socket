<template>
  <div class="view">
    <div class="content-view">
      <MessageItem v-for="item in 10" :key="item" class="message" />
    </div>
  </div>
</template>

<script setup>
import MessageItem from "@/components/atoms/MessageItem.vue";
</script>

<style lang="scss" scoped>
@import "@/assets/scss/variables.scss";
.view {
  background: white;
  width: 100%;
  height: 100%;
  padding: $p-1;
  overflow-y: auto;

  &::-webkit-scrollbar {
    width: 10px;
    border-radius: 10px;
  }

  &::-webkit-scrollbar-track {
    background: #f1f1f1;
    border-radius: 10px;
  }

  &::-webkit-scrollbar-thumb {
    background: $blue-2;
    border-radius: 10px;
    transition: 0.2s ease-in-out;
  }

  &::-webkit-scrollbar-thumb:hover {
    background: $blue-3;
    border-radius: 10px;
  }
  .message {
    margin-bottom: 1rem;
  }
}
</style>