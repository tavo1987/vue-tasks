<template>
    <div class="task-list">
        <template v-for="(task ,index) in tasks">
            <task-item :tasks="tasks" :task="task" :index="index"></task-item>
        </template>
        <task-form @pushTask="addTask"></task-form>
    </div>
</template>

<script>
    import TaskForm from './TaskForm.vue';
    import TaskItem from './TaskItem.vue';

    export default {

        data() {
            return {
                tasks: [
                    {
                        name: 'Task uno',
                        pending: false,
                    },
                    {
                        name: 'Task Dos',
                        pending: true,
                    },
                    {
                        name: 'Task Tres',
                        pending: true,
                    }
                ],
            }
        },

        created() {
            this.$bus.$on('removeTask', this.removeTask);
        },

        methods: {
            addTask(value) {
                this.tasks.push({
                    name: value,
                    pending: true,
                    editing: false,
                });
            },

            removeTask(index) {
                this.tasks.splice(index, 1);
            }
        },

        components: {
            'task-form': TaskForm,
            'task-item': TaskItem,
        }
    }
</script>

<style lang="scss">
    .complete {
        text-decoration: line-through;
    }

    .task-list {
        width: 100%;
    }
</style>
