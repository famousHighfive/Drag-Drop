<script setup>
const props = defineProps({
    task: {
        type: Object,
        required: true
    },
    // index: Number
})

const emit = defineEmits(['delete-task'])

function deleteTask(){
    emit('delete-task', props.task.id)
}
</script>


<template>

    <li class="item">
        <span>{{ task.id }}. {{ task.title }}</span>
        <button @click="deleteTask">❌</button>
    </li>

</template>


<style scoped>
.item{
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 1.5rem;
    margin-block: 0.6rem;
}

.item > span{
    font-size: 1.3rem;
    cursor: grab;
}

.item > button{
    background-color: transparent;
    cursor: pointer;
    border: none;
}

</style>