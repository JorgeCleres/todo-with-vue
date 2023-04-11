<template>
    <div class="tasks">
        <template v-if="tasks.length">
            <TaskComponent 
                v-for="(task, i) in tasks"
                @taskDeleted="$emit('taskDeleted', i)"
                @taskStateChanged="$emit('taskStateChanged', i)"
                :key="task.name"
                :task="task"    
            ></TaskComponent>
        </template>
        <p v-else class="no-task">Sua vida está em dia :)</p>
    </div>
</template>

<script>
import TaskComponent from './TaskComponent.vue'

export default {
    components: {TaskComponent},
    props: {
        tasks: { type: Array, required: true}
    }
}
</script>

<style>
    .tasks {
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .task-grid {
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
    }

    .task-grid .task {
        margin: 10px
    }

    .no-task {
        color: #b5b5b5;
        text-align: center;
        font-family: cursive;
    }
</style>