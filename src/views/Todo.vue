<template>
  <div>
    <img id="img1" alt="meta_think" src="../assets/meta_think.png" />
    <link rel="preconnect" href="https://fonts.gstatic.com" />
    <link
      href="https://fonts.googleapis.com/css2?family=Dela+Gothic+One&display=swap"
      rel="stylesheet"
    />
    <div id="font">Welcome Todo</div>
    <div id="font" class="w-1/2 mx-auto flex justify-center	mb-3 ">
      <input
        type="text "
        class="w-1/2 border	border-gray-700	"
        v-model="todoText"
        @keyup.enter="addTodo"
      />
      <button id="button1" class="mx-2.5" @click="addTodo">Upload</button>
    </div>
    <table class="border-separate border border-yellow-800 mx-auto w-1/2">
      <thead>
        <tr>
          <th class="border border-yellow-600 "></th>
          <th class="border border-yellow-600 w-1/4">Id</th>
          <th class="border border-yellow-600 w-1/2">할일</th>
          <th class="border border-yellow-600 w-1/4">delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="todo in todos" :key="todo.id">
          <td class="border border-yellow-600">
            <input
              class="inline-block align-middle"
              type="checkbox"
              :checked="todo.done"
              @click="doneTodo(todo)"
            />
          </td>
          <td class="border border-yellow-600">{{ todo.id }}</td>
          <td
            class="border border-yellow-600"
            :class="{ 'line-through': todo.done }"
          >
            {{ todo.text }}
          </td>
          <td class="border border-yellow-600">
            <button @click="deleteTodo(todo)">할일삭제</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
import axios from "axios";
export default {
  created() {
    this.getTodos();
  },
  data() {
    return {
      todos: [],
      todoText: "",
    };
  },
  methods: {
    async getTodos() {
      const result = await axios.get("http://localhost:3000/todo");
      this.todos = result.data;
      console.log(this.todos);
    },
    async addTodo() {
      if (this.todoText === "") return;
      console.log("todo");
      const newTodo = {
        text: this.todoText,
        done: false,
      };
      await axios.post(`http://localhost:3000/todo`, newTodo);
      this.getTodos();
      this.todoText = "";
    },
    async doneTodo(todo) {
      console.log("done", todo);
      await axios.patch(`http://localhost:3000/todo/${todo.id}`, {
        done: !todo.done,
      });
      this.getTodos();
    },
    async deleteTodo(todo) {
      console.log("todo");

      await axios.delete(`http://localhost:3000/todo/${todo.id}`);

      this.getTodos();
      this.todoText = "";
    },
  },
};
</script>
<style lang="scss" scoped>
div {
  text-align: center;
}
input {
  border-width: thick;
  border-color: gray;
}
table {
  border-width: thick;
  border-color: gray;
}
#img1 {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 300px;
  height: 100%;
  text-align: center;
}
#button1 {
  padding: 8px;
  background-color: gray;
  color: orange;
}
#font {
  font-family: "Dela Gothic One", cursive;
}
</style>
