<template>
    <div class="inputBox shadow">
        <input
            type="text"
            placeholder="Type what you have to do"
            v-model="newTodoItem"
            v-on:keyup.enter="addTodo"
        />
        <span v-on:click="addTodo">
            <i class="fa-solid fa-plus"></i>
        </span>

        <modal v-if="showModal" @close="showModal = false">
            <h3 slot="header">경고</h3>
            <span class="footerSpan" slot="footer" @click="showModal = false">
                할 일을 입력하세요.
                <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
            </span>
        </modal>
    </div>
</template>

<script>
import Modal from "./common/AlertModal.vue";

export default {
    data() {
        return {
            newTodoItem: "",
            showModal: false,
        };
    },
    methods: {
        addTodo() {
            //공백도 입력되는 상황을 막아주기 위해
            if (this.newTodoItem !== "") {
                let value = this.newTodoItem && this.newTodoItem.trim();
                this.$emit("addTodo", value);
                this.clearInput();
            } else {
                this.showModal = !this.showModal;
            }
        },
        clearInput() {
            //인풋박스 입력후 초기화
            this.newTodoItem = "";
        },
    },
    components: {
        Modal: Modal,
    },
};
</script>

<style scoped>
.inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}
span {
    float: right;
    background: linear-gradient(to right, #6677ff, #885bc7);
    width: 45px;
    border-radius: 0 5px 5px 0;
}
input {
    border: none;
    font-size: 1rem;
    text-align: center;
    width: calc(90% - 45px);
}
input:focus {
    outline: none;
}
i {
    color: white;
    vertical-align: middle;
}
.footerSpan {
    background: none;
    width: 100%;
    font-weight: 600;
    color: rgba(0, 0, 0, 0.527);
}
</style>
