<template>
  <div class="message">
    <div class="content-message">
      <span>
        {{ formatedInfo.message }}
      </span>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  props: {
    info: { type: [Object, String], required: true },
  },
  setup(props) {
    const formatedInfo = ref(props.info);
    if (typeof props.info == "string") {
      formatedInfo.value = JSON.parse(props.info);
    }
    return { formatedInfo };
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/scss/variables.scss";
.message {
  padding: $p-1 0;
 
  .content-message {
    background: $blue-3;
    display: inline ;
    padding: $p-1;
    border-radius: 10px;
     max-width: 100% !important;

    span {
      font-weight: 500;
      font-size: 0.9em;
      color: white;
      word-wrap:break-word;
    }

    @media (max-width: $mobile-2) {
      display: inline-block;
    }
  }
}
</style>
