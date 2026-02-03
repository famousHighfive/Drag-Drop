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
                <template #item="{ element }">
                    <Task :task="element" @delete-task="deleteTask" />
                </template>
            </draggableComponent>
        </div>
        <div>
            <h3>Tache terminée</h3>
            <draggableComponent :list="tasksCompleted" item-key="id" group="tasks"
                @update:list="emit('update:tasksCompleted', $event)" class="ul" >
                <template #item="{ element }">
                    <Task :task="element" @delete-task="deleteTask" />
                </template>
            </draggableComponent>
        </div>

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