<template>
    <div id="app">
        <TodoHeader></TodoHeader>
        <TodoInput v-on:addTodo="addTodo"></TodoInput>
        <TodoList
            v-bind:propsdata="todoItems"
            @removeTodo="removeItem"
        ></TodoList>
        <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
    </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";

export default {
    data() {
        return { todoItems: [] };
    },

    components: {
        TodoHeader: TodoHeader,
        TodoInput: TodoInput,
        TodoList: TodoList,
        TodoFooter: TodoFooter,
    },
    created: function () {
        if (localStorage.length > 0) {
            for (let i = 0; i < localStorage.length; i++) {
                this.todoItems.push(localStorage.key(i));
            }
        }
    },
    methods: {
        addTodo(todoItem) {
            localStorage.setItem(todoItem, todoItem);
            this.todoItems.push(todoItem);
        },
        clearAll() {
            localStorage.clear();
            this.todoItems = [];
        },
        removeItem(todoItem, index) {
            localStorage.removeItem(todoItem);
            this.todoItems.splice(index, 1);
        },
    },
};
</script>

<style>
@font-face {
    font-family: "GmarketSansBold";
    src: url("https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2001@1.1/GmarketSansBold.woff")
        format("woff");
    font-weight: normal;
    font-style: normal;
}
@font-face {
    font-family: "Pretendard-Light";
    src: url("https://cdn.jsdelivr.net/gh/Project-Noonnu/noonfonts_2107@1.1/Pretendard-Light.woff")
        format("woff");
    font-weight: 300;
    font-style: normal;
}
.shadow {
    box-shadow: 0 10px 10px rgba(0, 0, 0, 0.1);
}

body {
    background-color: gainsboro;
}

#app {
    font-family: "Pretendard-Light", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    max-width: 600px;
    margin: auto;
    padding: 30px 3vw;
}
</style>
