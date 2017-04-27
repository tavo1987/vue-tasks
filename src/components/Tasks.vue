<template>
    <div class="task-list">
        <div class="columns">
            <div class="column has-text-centered">
                <a href="#" @click.prevent="completeAllTask" class="button is-warning">Completar todas</a>
            </div>
            <div class="column has-text-centered">
                <a href="#" @click.prevent="deleteCompletedTask" class="button is-danger">Borrar completadas</a>
            </div>
        </div>

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
            },

            completeAllTask() {
                for ( let task of this.tasks){
                    task.pending = false;
                }
            },

            deleteCompletedTask() {
                let uncompletedTasks = this.tasks.filter( task => task.pending);
                this.tasks = uncompletedTasks;
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
