<template>
<div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <!-- <button v-on:click="addTodo">add</button> -->
    <span class="addContainer" v-on:click="addTodo">
        <i class="fas fa-plus addBtn"></i>
    </span>
</div>
</template>

<script>
export default {
    data: function () {
        return {
            newTodoItem: ""
        }
    },
    methods: {
        addTodo: function () {
            if (this.newTodoItem !== '') { // 값이 있을 때
                // this.$emit('이벤트 이름', 인자1, 인자2, ...);
                this.$emit('addTodoItem', this.newTodoItem); // 하위에서 addTodoItem 이벤트 발생 -> App.vue의 메서드 호출 

                this.clearInput();
            }
        },
        clearInput: function () {
            this.newTodoItem = '';

        }
    }
}
</script>

<style scoped>
input:focus {
    outline: none;
}

.inputBox {
    background-color: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}

.inputBox input {
    border-style: none;
    font-size: 0.9rem;
}

.addContainer {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}

.addBtn {
    color: white;
    vertical-align: middle;
}
</style>
