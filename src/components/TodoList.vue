<template>
  <div>
    <h1>Todo List</h1>
    <form @submit.prevent="handleSubmit">
      <label>Title:</label>
      <input 
        v-model="inputTitle"
        placeholder="Write your title..."
        required
      />
      <label>Description:</label>
      <input 
        v-model="inputDescription"
        placeholder="Write your description..."
        required
      />
      <button type="submit">{{ isEditing ? 'Update' : 'Add' }}</button>
    </form>

    <div v-for="todo in todos" :key="todo.id">
      <div v-if="isEditing && todo.id === currentTodoId">
        <!-- Inputs for editing -->
        <label>Title:</label>
        <input 
          v-model="editTitle"
          placeholder="Write your title..."
          required
        />
        <label>Description:</label>
        <input 
          v-model="editDescription"
          placeholder="Write your description..."
          required
        />
        <button @click="handleUpdate">Update</button>
      </div>
      <div v-else>
        <!-- Display todo items -->
        <input type="checkbox" @click="toggleComplete(todo)" v-model="todo.completed">
        <h2 :class="{ completed: todo.completed }">{{ todo.title }}</h2>
        <p :class="{ completed: todo.completed }">{{ todo.description }}</p>
        <button @click="handleEdit(todo)">Edit</button>
        <button @click="handleDelete(todo.id)">Delete</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  data() {
    return {
      inputTitle: '',
      inputDescription: '',
      todos: [],
      isEditing: false,
      currentTodoId: null,
      editTitle: '',
      editDescription: ''
    }
  },
  methods: {
    handleSubmit() {
      if (this.inputTitle.trim() && this.inputDescription.trim()) {
        if (this.isEditing) {
          this.handleUpdate();
        } else if(this.editTitle !== '') {
          this.todos.push({
            id: Date.now(),
            title: this.editTitle,
            description: this.editDescription,
            completed: false
          });
        } 
        else {
          // Add a new todo item
          this.todos.push({
            id: Date.now(),
            title: this.inputTitle,
            description: this.inputDescription,
            completed: false
          });
          this.resetForm();
        }
      }
    },
    handleUpdate() {
      const todoIndex = this.todos.findIndex(todo => todo.id === this.currentTodoId);
      if (todoIndex !== -1) {
        this.todos[todoIndex].title = this.editTitle;
        this.todos[todoIndex].description = this.editDescription;
        this.resetForm();
      }
    },
    resetForm() {
      this.inputTitle = '';
      this.inputDescription = '';
      this.isEditing = false;
      this.currentTodoId = null;
    },
    toggleComplete(todo) {
      todo.completed = !todo.completed;
    },
    handleDelete(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    handleEdit(todo) {
      this.editTitle = todo.title;
      this.editDescription = todo.description;
      this.isEditing = true;
      this.currentTodoId = todo.id;
    }
  }
}
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}
</style>
