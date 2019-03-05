<template>
<div>
    <ul>
        <li v-for="todoItem in todoItems" v-bind:key="todoItem" class="shadow">
            {{ todoItem }}
        <span class="removeBtn" v-on:click="removeTodo">
            <i class="fas fa-trash-alt"></i>
        </span>
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
    method: {
        removeTodo: function () {
            
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
ul {
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left;
}
li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
}
.checkBtn {
    line-height: 45px;
    color: #62acde;
    margin-right: 5px;
}
.checkBtnCompleted {
    color: #b3adad;
}
.textCompleted {
    text-decoration: line-through;
    color: #b3adad;
}
.removeBtn {
    margin-left: auto;
    color: #de4343
}

</style>
