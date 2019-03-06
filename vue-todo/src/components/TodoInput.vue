<template>
<div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <!-- <button v-on:click="addTodo">add</button> -->
    <span class="addContainer" v-on:click="addTodo">
        <i class="fas fa-plus addBtn"></i>
    </span>

    <!-- slot: 특정 컴포넌트의 일부 UI를 재사용하는 기능 -->
    <Modal v-if="showModal" @close="showModal = false">
        <!--    
        you can use custom content here to overwrite
        default content
        -->
        <h3 slot="header">경고!
            <!-- Modal이 사라지도록 -->
            <i class="closeModalBtn fas fa-times" @click="showModal = false"></i>
        </h3>
        <div slot="body">무언가를 입력하세요.</div>
    </Modal>
</div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
    data() {
        return {
            newTodoItem: "",
            showModal: false
        }
    },
    methods: {
        addTodo() {
            if (this.newTodoItem !== '') { // 값이 있을 때
                // this.$emit('이벤트 이름', 인자1, 인자2, ...);
                this.$emit('addTodoItem', this.newTodoItem); // 하위에서 addTodoItem 이벤트 발생 -> App.vue의 메서드 호출 

                this.clearInput();
            } else {
                this.showModal = !this.showModal;
            }
        },
        clearInput() {
            this.newTodoItem = '';

        }
    },
    components: {
        Modal: Modal,

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
.closeModalBtn {
    color: #42b983;
}
</style>

