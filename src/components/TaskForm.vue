<template>
    <form @submit.prevent="submit" class="columns">
        <div class="column is-8">
            <input v-model="newTask" type="text" class="input" @keyUp.enter="submit">
        </div>
        <div class="column">
            <button :disabled="this.newTask == ''" class="button is-primary" type="submit">Add task</button>
        </div>
    </form>
</template>

<script>
export default {
    data() {
        return {
            newTask: '',
        }
    },
    methods: {
        submit() {
            this.$emit('pushTask', this.newTask);
            this.newTask = '';
        }
    }
}
</script>
