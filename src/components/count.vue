<script setup>
import { ref,defineProps} from 'vue';
const count = ref(0);

const increaseCounter = () => {
    count.value++;
}

defineProps({
    messageText: String,
    changeMessage: Function
})

const message = ref('');



</script>
<template>
    <div>Hello {{ messageText }}</div>
    <input type="text" v-model="message">
    <button @click = "changeMessage(message)">change message from count</button>
    
    <button @click="increaseCounter"> Click {{ count }}</button>
</template>
<style>
</style>