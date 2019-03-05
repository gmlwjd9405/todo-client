<template>
<div>
    <ul>
        <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem.item" class="shadow">
            <i class="checkBtn fas fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}" 
                    v-on:click="toggleComplete(todoItem, index)"></i>
            <!-- {{obj.속성값}} 을 가져온다. -->
            <!-- todoItem.completed가 true일 때 class로 textCompleted를 넣는다.  -->
            <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
            <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
            <i class="fas fa-trash-alt"></i>
        </span>
        </li>
    </ul>
</div>
</template>

<script>
export default {
    props: ['propsdata'],
    methods: {
        removeTodo: function (todoItem, index) {
            console.log(todoItem, index);
            localStorage.removeItem(todoItem);
            // 해당 item을 지우고 새로운 배열을 반환 -> 화면에서도 삭제된다.
            this.todoItems.splice(index, 1);
        },
        toggleComplete: function (todoItem, index) {
            console.log(todoItem);
            todoItem.completed = !todoItem.completed;

            // [localStorage 갱신] 자동으로 localStorage를 업데이트하는 API가 없음 (삭제 후 다시 저장)
            localStorage.removeItem(todoItem.item);
            localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
        }
    },

}
</script>

<style scoped>
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
