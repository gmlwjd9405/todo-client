<template>
<!-- HTML -->
<div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput></TodoInput>
    <!-- v-bind:내려보낼 프롭스 속성 이름="현재 위치의 컴포넌트 데이터 속성" -->
    <TodoList v-bind:propsdata="todoItems"></TodoList>
    <TodoFooter></TodoFooter>
</div>
</template>

<script>
// js script
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
    // localStorage의 값을 담을 data - 대부분의 Component가 활용 
    data: function () {
        return {
            todoItems: []
        }
    },
    created: function () {
        if (localStorage.length > 0) {
            for (var i = 0; i < localStorage.length; i++) {
                if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
                    // [데이터 가져오기] string 값을 obj로 변환해서 가져온다.
                    this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
                    // this.todoItems.push(localStorage.key(i));
                }
            }
        }
    },
    components: {
        // 컴포넌트 태그명 : 컴포넌트 내용
        'TodoHeader': TodoHeader,
        'TodoInput': TodoInput,
        'TodoList': TodoList,
        'TodoFooter': TodoFooter,

    }

}
</script>

<style>
/* css */
body {
    text-align: center;
    background-color: #F6F6F6;
}

input {
    border-style: groove;
    width: 200px;
}

button {
    border-style: groove;
}

.shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>
