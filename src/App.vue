<template>
    <div id="app" class="container">
        <div class="columns">
            <div class="column is-6 is-offset-3">
                <div class="panel">
                    <div class="panel-heading">
                        Task List
                    </div>
                    <div class="panel-block">
                        <tasks></tasks>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

import Tasks from './components/Tasks.vue';
export default {
    name: 'app',
    data () {
        return {
            msg: 'Welcome to Your Vue.js App'
        }
    },
    components : {
        'tasks': Tasks,
    }
}
</script>

<style lang="scss">
    body {
        padding-top: 2rem;
    }
</style>
