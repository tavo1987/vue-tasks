<template>
    <div class="columns">
        <div class="column is-2">
            <a @click="complete"  href="#" class="button">
                <app-icon :icon="task.pending ?  'square-o' :  'check-square-o' "></app-icon>
            </a>
        </div>

        <div class="column is-7">
            <span v-if="!task.editing" :class="{ complete: !task.pending }">{{task.name}}</span>
            <input class="input" v-else type="text" name="task" v-model="drafTask">
        </div>

        <div class="column is-3">
            <template v-if="task.editing">
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
                drafTask : '',
            }
        },

        methods: {
            complete() {
                this.task.pending = !this.task.pending;
            },

            remove() {
                //this.$emit('remove', this.index);
                this.$bus.$emit('remove', this.index);
            },

            edit() {
                this.$emit('edit');
                this.task.editing = true;
                this.drafTask = this.task.name
            },

            cancelEdit() {
                this.task.editing = false;
                this.drafTask.name = this.task.name;
            },

            update() {
                this.task.name = this.drafTask;
                this.task.editing = false;
            },
        }
    }
</script>
