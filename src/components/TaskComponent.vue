<template>
    <div class="task" :class="stateClass" @click="$emit('taskStateChanged', task)" >
        <span @click="$emit('taskDeleted', task)" class="close">x</span>
        <p>{{ task.name }}</p>
    </div>
</template>

<script>
export default {
    props: {
        task: { type: Object, required: true}
    },
    computed: {
        stateClass() {
            return {
                pending: this.task.pending,
                done: !this.task.pending,
            }
        }
    }
}
</script>

<style scoped>
    .task {
        box-sizing: border-box;
        width: 350px;
        height: 150px;
        padding: 10px;
        border-radius: 8px;
        font-size: 2rem;
        font-weight: 300;
        cursor: pointer;
        user-select: none;
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 0 10px;
    }

    .pending {
        border-left: 12px solid rgb(247, 0, 0);
        background-color: rgb(255, 112, 112);
    }

    .done {
        border-left: 12px solid rgb(60, 255, 92);
        background-color: rgb(153, 252, 170);
        color: grey;
        text-decoration: line-through;
    }

    span.close {
        position: relative;
        bottom: 46%;
        left: 59%;
        background: #0000004d;
        border-radius: 50px;
        font-size: 17px;
        width: 20px;
        text-align: center;
        color: white;
        font-family: sans-serif;
    }

    p {
        color: wheat;
        font-family: cursive;
    }
</style>