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
                // 체크 유무, text에 대한 객체 
                var obj = {
                    completed: false,
                    item: this.newTodoItem
                };
                // 저장하는 로직 (JS 객체를 Srting으로 변환)
                localStorage.setItem(this.newTodoItem, JSON.stringify(obj));
                // localStorage.setItem(this.newTodoItem, obj);
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
