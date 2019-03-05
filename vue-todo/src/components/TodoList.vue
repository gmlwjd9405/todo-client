<template>
<div>
    <ul>
        <li v-for="todoItem in todoItems" v-bind:key="todoItem">
            {{ todoItem }}
        </li>
    </ul>
</div>
</template>

<script>
export default {
    // localStorage의 값을 담을 data
    data: function () {
        return {
            todoItems: []
        }
    },
    created: function () {
        if (localStorage.length > 0) {
            for (var i = 0; i < localStorage.length; i++) {
                if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
                    this.todoItems.push(localStorage.key(i));
                }
            }
        }

    }

}
</script>

<style>

</style>
