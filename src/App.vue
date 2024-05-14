<template>
  <div>
    <div class="h1">
      <h1><b>Daftar Nama Mahasiswa</b></h1>
    </div>
    <input
      type="text"
      v-model="newTodo"
      @keyup.enter="addTodo"
      placeholder="Masukkan Nama..."
    />
    <ul>
      <li
        v-for="(todo, index) in todos"
        :key="index"
        :class="{ completed: todo.completed }"
      >
        <span v-if="!todo.editing" @click="toggleCompleted(todo)">
          {{ todo.text }}
        </span>
        <input
          v-else
          type="text"
          v-model="todo.text"
          @keyup.enter="finishEdit(todo)"
          @blur="finishEdit(todo)"
        />
        <div class="button-group">
          <button @click="editTodo(todo)" :class="{ edit: !todo.editing }">
            {{ todo.editing ? "Save" : "Edit" }}
          </button>
          <button @click="removeTodo(todo)">Delete</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: "",
      todos: [],
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== "") {
        this.todos.push({
          text: this.newTodo,
          completed: false,
          editing: false,
        });
        this.newTodo = "";
      }
    },
    removeTodo(todo) {
      const index = this.todos.indexOf(todo);
      if (index !== -1) {
        this.todos.splice(index, 1);
      }
    },
    toggleCompleted(todo) {
      if (!todo.editing) {
        todo.completed = !todo.completed;
      }
    },
    editTodo(todo) {
      todo.editing = !todo.editing;
      if (!todo.editing && todo.text.trim() === "") {
        this.removeTodo(todo);
      }
    },
    finishEdit(todo) {
      todo.editing = false;
      if (todo.text.trim() === "") {
        this.removeTodo(todo);
      }
    },
  },
};
</script>

<style scoped>
body {
  font-family: "Roboto", sans-serif;
  font-style: bold;
  background-color: #f9fafb;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
#app {
  width: 500px;
  max-width: 1000px;
  background-color: #440240;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
h1 {
  text-align: center;
  color: #ffffff;
  padding: 20px;
}
input[type="text"] {
  width: calc(100% - 40px);
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin-bottom: 8px;
  padding: 10px;
  background-color: #f2f4f8;
  border-radius: 4px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.completed {
  text-decoration: line-through;
  color: #999;
}
.button-group {
  display: flex;
  gap: 10px;
}
button {
  padding: 6px 10px;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
}
button:hover {
  opacity: 0.9;
}
button.edit {
  background-color: blue;
}
button.edit:hover {
  background-color: darkblue;
}
button:not(.edit) {
  background-color: red;
}
button:not(.edit):hover {
  background-color: rgb(190, 0, 0);
}
</style>
