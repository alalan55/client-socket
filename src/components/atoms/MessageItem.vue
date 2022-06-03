<template>
    <div class="message">
        <div class="content-message">
           <span>
               {{message}}
           </span>
        </div>
    </div>
</template>

<script setup>
const props = defineProps({
    message: {type: String, default: 'Insira uma mensagem'}
})
</script>

<style lang="scss" scoped>
@import "@/assets/scss/variables.scss";
.message{
    // border: 1px solid;
    padding: $p-1 0;
    .content-message{
        background: $blue-3;
        display: inline;
        padding: $p-1;
        border-radius: 10px;

        span{
            font-weight: 500;
            font-size: .9em;
            color: white;
        }

        @media (max-width: $mobile-2){
            display: inline-block;
        }
    }
}

</style>