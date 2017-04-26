<template>
    <div class="columns">
        <div class="column is-2">
            <a @click="complete"  href="#" class="button">
                <app-icon :icon="task.pending ?  'square-o' :  'check-square-o' "></app-icon>
            </a>
        </div>

        <div class="column is-7">
            <span v-if="!editing" :class="{ complete: !task.pending }">{{task.name}}</span>
            <input class="input" v-else type="text" name="task" v-model="drafTask">
        </div>

        <div class="column is-3">
            <template v-if="editing">
                <a href="#" @click="update" class="button is-primary">
                    <app-icon icon="check"></app-icon>
                </a>
                <a href="#" @click="cancelEdit" class="button is-danger">
                    <app-icon icon="times"></app-icon>
                </a>
            </template>

            <template v-else>
                <a href="#" @click="edit" class="button is-info">
                    <app-icon icon="pencil"></app-icon>
                </a>
                <a href="#" @click="remove" class="button is-danger">
                    <app-icon icon="trash"></app-icon>
                </a>
            </template>
        </div>
    </div>
</template>

<script>
    import Icon from './Icon.vue';
    import EventBus from '../EventBus.js';
    export default {
        props: ['task', 'index'],
        components: {
            'app-icon': Icon,
        },

        data() {
            return {
                editing : false,
                drafTask : '',
            }
        },

        created() {
            this.$bus.$on('editingTask', task => this.editing = false);
        },

        methods: {
            complete() {
                this.task.pending = !this.task.pending;
            },

            remove() {
                this.$bus.$emit('removeTask', this.index);
            },

            edit() {
                this.$bus.$emit('editingTask', this.task);
                this.editing = true;
                this.drafTask = this.task.name
            },

            cancelEdit() {
                this.editing = false;
                this.drafTask = this.task.name;
            },

            update() {
                this.task.name = this.drafTask;
                this.editing = false;
            },
        }
    }
</script>
