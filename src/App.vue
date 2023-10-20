<template>
  <div id="app" class="container mx-auto p-4">
    <h1 class="text-2xl font-bold mb-4">Todo App</h1>

    <div class="flex mb-4">
      <input type="text" v-model="newTodo" class="border border-gray-300 rounded-l px-2 py-1 w-full">
      <button @click="addTodo" class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-1 rounded-r">Add</button>
    </div>

    <ul>
      <li v-for="todo in todos" :key="todo.id" class="flex items-center mb-2">
        <span class="mr-2">{{ todo.title }}</span>
        <button @click="editTodo(todo.id)" class="bg-yellow-500 hover:bg-yellow-600 text-white px-2 py-1 rounded">Edit</button>
        <button @click="deleteTodo(todo.id)" class="bg-red-500 hover:bg-red-600 text-white px-2 py-1 rounded">Delete</button>
      </li>
    </ul>

    <div v-if="editingTodo">
      <input type="text" v-model="editedTodo" class="border border-gray-300 rounded-l px-2 py-1 w-full">
      <button @click="updateTodo" class="bg-green-500 hover:bg-green-600 text-white px-4 py-1 rounded-r">Update</button>
      <button @click="cancelEdit" class="bg-gray-500 hover:bg-gray-600 text-white px-4 py-1 rounded">Cancel</button>
    </div>
  </div>
</template>

  <script setup>
    const app = Vue.createApp({
      data() {
        return {
          newTodo: '',
          editedTodo: '',
          editingIndex: null,
          todos: [
            { id: 1, title: 'Todo 1' },
            { id: 2, title: 'Todo 2' },
            { id: 3, title: 'Todo 3' }
          ],
        };
      },
      methods: {
        addTodo() {
          if (this.newTodo.trim() !== '') {
            const newId = this.todos.length + 1;
            this.todos.push({ id: newId, title: this.newTodo });
            this.newTodo = '';
          }
        },
        deleteTodo(index) {
          this.todos.splice(index, 1);
        },
        editTodo(index) {
          this.editingIndex = index;
          this.editedTodo = this.todos[index].title;
        },
        saveTodo() {
          if (this.editedTodo.trim() !== '') {
            this.todos[this.editingIndex].title = this.editedTodo;
            this.cancelEdit();
          }
        },
        cancelEdit() {
          this.editingIndex = null;
          this.editedTodo = '';
        },
      },
    });

    app.mount('#app');
  </script>

<style lang="scss" scoped>

</style>