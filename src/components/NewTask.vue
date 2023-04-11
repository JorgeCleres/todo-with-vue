<template>
    <div class="new-task">
        <input v-model="name" @keydown.enter="add" type="text">
        <button @click="add">+</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            name: ''
        }
    },
    methods: {
        add() {
            this.$emit('taskAdded', { name: this.name})
            this.name = ''
        }
    }
}
</script>

<style>

    .new-task {
        margin-bottom: 15px
    }

    input {
        background: transparent;
        border: 1px solid white;
        height: 25px;
        width: 300px;
        border-radius: 5px;
        font-size: 20px;
        font-family: cursive;
        color: white;
        padding: 7px;
    }

    button {
        height: 31px;
        width: 32px;
        color: white;
        font-size: 18px;
        background: #074c6a;
        border: 1px solid white;
        border-radius: 30px;
        margin: 0px 5px 0;
        padding: 0px;
    }

</style>