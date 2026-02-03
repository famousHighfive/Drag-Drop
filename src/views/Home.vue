<script setup>
import DisplayTask from '@/components/DisplayTask.vue';
import Form from '@/components/Form.vue';
import { ref } from 'vue';

// Tableau principal
const tasks = ref([])
const completedTasks = ref([])


// Function pour recuperer la tache
// Inserer un id 
// Ajouter un status isDone
function addTask(task){
    tasks.value.push({
        ...task,
        id: Date.now()
        })    
}

function deleteTask(id){
    tasks.value = tasks.value.filter(task => task.id !== id)
    completedTasks.value = completedTasks.value.filter(task => task.id !== id)
}

</script>


<template>
    <!-- Formulaire d'entrée des données -->
    <Form @ajout-task="addTask" />

    <!-- Conteneur d'affichage des tasks -->
    <DisplayTask v-model:tasks="tasks" v-model:tasksCompleted="completedTasks" @delete-task="deleteTask" />

</template>


<style scoped>


</style>