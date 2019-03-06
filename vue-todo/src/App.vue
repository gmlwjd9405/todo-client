<template>
<!-- HTML -->
<div id="app">
    <TodoHeader></TodoHeader>
    <!-- v-on:하위 컴포넌트에서 발생시킨 이벤트 이름="현재 컴포넌트 메서드 명" -->
    <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
    <!-- v-bind:내려보낼 프롭스 속성 이름="현재 위치의 컴포넌트 데이터 속성" -->
    <TodoList v-bind:propsdata="todoItems" v-on:removeItem="removeOneItem" v-on:toggleItem="toggleOneItem"></TodoList>
    <TodoFooter v-on:clearAll="clearAllItems"></TodoFooter>
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
    data() {
        return {
            todoItems: []
        }
    },
    methods: {
        // 하위에서 받아온 인자값(this.newTodoItem)
        addOneItem(todoItem) {
            // 체크 유무, text에 대한 객체 
            const obj = {
                completed: false,
                item: todoItem
            };
            // [데이터 보내기] 저장하는 로직 (JS 객체를 Srting으로 변환)
            localStorage.setItem(todoItem, JSON.stringify(obj));

            // localStorage의 값과 화면의 값을 동기화 (push: 배열요소를 추가하는 JS API)
            this.todoItems.push(obj);
        },
        removeOneItem(todoItem, index) {
            // localStorage에서도 값을 삭제 (todoItem: obj, todoItem.item: 속성(key값과 동일하게 세팅함))
            localStorage.removeItem(todoItem.item); // key값에 접근해서 삭제 
            // 해당 item을 지우고 새로운 배열을 반환 -> 화면에서도 삭제된다.
            this.todoItems.splice(index, 1);
        },
        toggleOneItem(todoItem, index) {
            // todoItem.completed = !todoItem.completed;
            this.todoItems[index].completed = !this.todoItems[index].completed;

            // [localStorage 갱신] 자동으로 localStorage를 업데이트하는 API가 없음 (삭제 후 다시 저장)
            localStorage.removeItem(todoItem.item);
            localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
        },
        clearAllItems() {
            localStorage.clear();
            this.todoItems = []; // 빈 배열로 만들어서 화면을 갱신 
        }
    },
    created() {
        if (localStorage.length > 0) {
            for (let i = 0; i < localStorage.length; i++) {
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
        TodoHeader,
        TodoInput,
        TodoList,
        TodoFooter,
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
