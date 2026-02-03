<script setup>
import draggableComponent from 'vuedraggable';
import Task from './Task.vue';

const props = defineProps({
    tasks: {
        type: Array,
        required: true
    },
    tasksCompleted: {
        type: Array,
        required: true
    }
})

const emit = defineEmits(['delete-task', 'update:tasks', 'update:tasksCompleted'])

function deleteTask(id) {
    emit('delete-task', id)
}

</script>


<template>

    <div v-if="tasks.length || tasksCompleted.length" class="container">
        <div>
            <h3>Tache a faire</h3>
            <draggableComponent :list="tasks" item-key="id" group="tasks" @update:list="emit('update:tasks', $event)" class="ul" >
                <template #item="{ element, index }">
                    <Task :task="element" :index="index + 1" @delete-task="deleteTask" />
                </template>
            </draggableComponent>
        </div>
        <div>
            <h3>Tache terminée</h3>
            <draggableComponent :list="tasksCompleted" item-key="id" group="tasks"
                @update:list="emit('update:tasksCompleted', $event)" class="ul" >
                <template #item="{ element, index }">
                    <Task :task="element" :index="index + 1" @delete-task="deleteTask" />
                </template>
            </draggableComponent>
        </div>
<!-- 
        Imaginons que tu déplaces une tâche dans la colonne "À faire" :
Étape A (Dans vuedraggable) : L'utilisateur lâche la souris. La bibliothèque calcule le nouvel ordre et émet son signal interne @update:list.
Étape B (Dans DisplayTask) : Ton code intercepte @update:list. Il exécute immédiatement l'ordre : emit('update:tasks', $event). Il envoie donc le nouveau tableau vers le haut.
Étape C (Dans le Parent) : Grâce au v-model:tasks, le parent attrape ce tableau et écrase sa variable tasks.value avec le nouveau contenu.
Étape D (Le rendu) : Comme tasks est un ref(), Vue remarque le changement et redessine l'interface. La tâche apparaît déplacée. -->

<!-- Parce que tu as deux listes à gérer (tasks et tasksCompleted).
v-model:tasks cible la prop tasks.
v-model:tasksCompleted cible la prop tasksCompleted.
Cela permet de mettre à jour la bonne valise au bon moment. -->


    </div>
    <p class="pContainer" v-else>Aucune tache actuellement ❌</p>
</template>


<style scoped>
.container {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
}

.pContainer {
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 1.5rem;
}

h3{
    text-align: center;
}

.ul {
    display: flex;
    flex-direction: column;
    list-style: none;
    min-height: 300px;
    border-right: 1px solid;
}
</style>