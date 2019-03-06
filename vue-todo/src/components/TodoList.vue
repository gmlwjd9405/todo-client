<template>
<div>
    <transition-group name="list" tag="ul">
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
    </transition-group>
</div>
</template>

<script>
export default {
    props: ['propsdata'],
    methods: {
        removeTodo: function (todoItem, index) {
            console.log(todoItem, index);
            // removeItem 이벤트를 발생시키고, todoItem과 index 인자값을 전달한다.
            this.$emit('removeItem', todoItem, index);
        },
        toggleComplete: function (todoItem, index) {
            console.log(todoItem);
            this.$emit('toggleItem', todoItem, index);
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

/* transition-group name(list) todoItem List에 trasition 효과 */
.list-enter-active, .list-leave-active {
    transition: all 1s; /* 1초 지속 */
}

.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
    opacity: 0;
    transform: translateY(30px);
}
</style>
