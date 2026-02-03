<script setup>
import { reactive } from 'vue';

// Gestion des données réactives
const form = reactive({
    title: ''
})

// initialisation dun evenement emit
const emit = defineEmits(['ajout-task'])

// Function dajout dune tache
function submitForm(){
    // Bloquer lajout quand lentrée est vide
    if(!form.title.trim()) return

    // Envoyer la donnée vers le parent
    emit('ajout-task', {...form})

    // Reinitialiser les champs
    form.title = ''
}

</script>


<template>

    <form @submit.prevent="submitForm" class="form">
        <input type="text" v-model="form.title" placeholder="Entrer une tâche" class="inputForm" />
        <button type="submit" class="btnForm">Create</button>
    </form>

</template>


<style scoped>
.form {
    display: flex;
    justify-content: center;
    gap: 1rem;
    flex-wrap: wrap;
    margin-top: 1.9rem;
}

.inputForm {
    padding: 1rem 1.5rem;
    border-radius: 10px;
    border: 1px solid;
    min-width: 250px;
    font-size: 1rem;
}

.btnForm {
    background-color: cyan;
    padding: 1rem 1.5rem;
    border-radius: 10px;
    border: none;
    color: white;
    font-size: 1.4rem;
    cursor: pointer;
    transition: 0.3s;
}
</style>