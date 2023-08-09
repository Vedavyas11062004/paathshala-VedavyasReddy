<template>
  <div class="card" v-for="item in todos" :key="item.id">
    <!-- <img :src="imageSrc" class="card-img-top" :alt="altText" /> -->
    <div class="card-body">
      <h5 class="card-title">{{ item.name }}</h5>
      <p class="card-text">{{ item.email }}</p>
      <p class="card-text">{{ item.phoneno }}</p>
      <p class="card-text">{{ item.jobTitle }}</p>
      <p class="card-text">{{ item.comment }}</p>
      <a href="#" class="btn btn-primary">Veiw Profile</a>
    </div>
  </div>
</template>

<script>
import { API } from "aws-amplify";
import { listTodos } from "../graphql/queries";
import { onCreateTodo } from "../graphql/subscriptions";

export default {
  data() {
    return {
      todos: [],
    };
  },
  async created() {
    this.getTodos();
    this.subscribe();
  },
  methods: {
    async getTodos() {
      const todos = await API.graphql({
        query: listTodos,
      });
      console.log(todos.data.listTodos.items);
      this.todos = todos.data.listTodos.items;
    },
    subscribe() {
      API.graphql({ query: onCreateTodo }).subscribe({
        next: (eventData) => {
          let todo = eventData.value.data.onCreateTodo;
          if (this.todos.some((item) => item.name === todo.name)) return;
          this.todos = [...this.todos, todo];
        },
      });
    },
  },
};
</script>

<style scoped>
.card {
  width: 18rem;
  border: 1px solid #ccc;
  border-radius: 5px;
  overflow: hidden;
  margin: 20px;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.1);
}

.card-img-top {
  max-height: 200px;
  object-fit: cover;
}

.card-body {
  padding: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.card-title {
  font-size: 1.25rem;
  margin-bottom: 0.5rem;
}

.card-text {
  color: #666;
  margin-bottom: 0rem;
}

.btn-primary {
  background-color: rgb(68, 57, 204);
  border: none;
  color: white;
  padding: 0.5rem 1rem;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 1rem;
  border-radius: 5px;
  margin-block: 1rem;
  width: 100%;
}
</style>
