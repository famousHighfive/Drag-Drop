<script setup>
import { onMounted } from 'vue';
defineProps({
    message: String
})

const emit = defineEmits(['close']);

// Auto-fermeture après 3 secondes
// Quand le composant notification est monté, 3s apres je declenche levenement close
onMounted(() => {
    setTimeout(() => {
        emit('close');
    }, 3000);
});

</script>


<template>

<div class="notif">
    <p>{{ message }}</p>
</div>

</template>


<style scoped>
.notif{
    position: fixed;
    top: 20px;
    right: 20px;
    background-color: rgb(76, 134, 18);
    color: white;
    font-size: 1rem;
    padding: 0.3rem 1rem;
    border-radius: 8px;
    z-index: 1000;
}
</style>