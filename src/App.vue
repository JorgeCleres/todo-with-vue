<template>
    <div id="app">
        <h1>Tarefas</h1>
        <TaskProgress :progress="progress" />
        <NewTask @taskAdded="addTask" />
        <TaskGrid
            @taskDeleted="deleteTask"
            @taskStateChanged="toggleTaskState"
            :tasks="tasks"
        />
    </div>
</template>

<script>
import TaskGrid from './components/TaskGrid.vue'
import NewTask from './components/NewTask.vue'
import TaskProgress from './components/TaskProgress.vue'


export default {
    components: { TaskGrid, NewTask, TaskProgress },
    name: 'App',
    data() {
        return {
            tasks: []
        }
    },
    computed: {
        progress() {
            const total = this.tasks.length
            const done = this.tasks.filter(t => !t.pending).length
            return Math.round(done / total * 100) || 0
        }
    },
    watch: {
        tasks: {
            //verificar tudo que foi mexido de forma profunda
            deep: true,
            handler() {
                localStorage.setItem('tasks', JSON.stringify(this.tasks))
            }
        }
    },
    methods: {
        addTask(task) {
            // sameName == funcao
            const sameName = t => t.name === task.name
            const reallyNew = this.tasks.filter(sameName).length == 0
            if (reallyNew) {
                this.tasks.push({
                    name: task.name,
                    pending: task.pending || true
                })
            }
        },
        deleteTask(i) {
            this.tasks.splice(i, 1)
        },
        toggleTaskState(i) {
            this.tasks[i].pending = !this.tasks[i].pending
        }
    },
    created() {
        const json = localStorage.getItem('tasks')
        const array = JSON.parse(json)
        this.tasks = Array.isArray(array) ? array : []
    }
}
</script>

<style>
    body {
        background: rgb(2,0,36);
        background: linear-gradient(42deg, rgba(2,0,36,1) 0%, rgba(9,92,121,1) 56%, rgba(0,212,255,1) 100%);
    }

    #app {
        display: flex;
        flex: 1;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100vh
    }
    
    h1 {
        text-align: center;
        font-size: 3rem;
        font-family: cursive;
        color: white;
        font-weight: 100;
    }
</style>
