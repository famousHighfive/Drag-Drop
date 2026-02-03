<script setup>
import DisplayTask from '@/components/DisplayTask.vue';
import Form from '@/components/Form.vue';
import Notification from '@/components/Notification.vue';
import { ref } from 'vue';

// Tableau principal
const tasks = ref([])
const completedTasks = ref([])
const showNotif = ref(false); // État pour la visibilité

// Function pour recuperer la tache
// Inserer un id 
// Ajouter un status isDone
function addTask(task) {
    tasks.value.push({
        ...task,
        id: Date.now()
    })

    // Afficher la notif
    showNotif.value = true;
}


function deleteTask(id) {
    tasks.value = tasks.value.filter(task => task.id !== id)
    completedTasks.value = completedTasks.value.filter(task => task.id !== id)
}

</script>


<template>

    <Transition name="fade">
        <Notification v-if="showNotif" message="Tâche ajoutée avec succès ! ✅" @close="showNotif = false" />
    </Transition>
    <!-- Formulaire d'entrée des données -->
    <Form @ajout-task="addTask" />

    <!-- Conteneur d'affichage des tasks -->

    <!-- Donne la variable tasks à l'enfant (via la prop tasks). -->
    <!-- Écoute si l'enfant crie @update:tasks. -->
    <!-- Si l'enfant crie, prends la valeur reçue ($event) et mets-la dans la variable tasks du parent. -->
    <DisplayTask v-model:tasks="tasks" v-model:tasksCompleted="completedTasks" @delete-task="deleteTask" />

</template>


<style scoped>
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.5s;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>