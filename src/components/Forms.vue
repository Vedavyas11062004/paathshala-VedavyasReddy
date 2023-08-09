<template>
  <form class="row g-3" @submit.prevent="submitForm">
    <div class="col-md-6">
      <label for="inputText" class="form-label">Name:</label>
      <input
        type="text"
        class="form-control"
        id="inputText"
        v-model="formData.name"
      />
    </div>
    <div class="col-md-6">
      <label for="inputEmail4" class="form-label">Email:</label>
      <input
        type="email"
        class="form-control"
        id="inputEmail4"
        v-model="formData.email"
      />
    </div>
    <div class="col-md-6">
      <label for="inputNumber" class="form-label">Phone No:</label>
      <input
        type="text"
        class="form-control"
        id="inputNumber"
        v-model="formData.phoneno"
      />
    </div>
    <div class="col-md-6">
      <label for="inputJob" class="form-label">Job Title:</label>
      <input
        type="text"
        class="form-control"
        id="inputJob"
        v-model="formData.jobTitle"
      />
    </div>
    <div class="col-md-6">
      <label for="inputState" class="form-label">Types of Job:</label>
      <select id="inputState" class="form-select" v-model="formData.state">
        <option value="" disabled selected>Choose...</option>
        <option>Full time</option>
        <option>Half time</option>
        <option>Remote</option>
        <option>In office</option>
      </select>
    </div>
    <div class="col-12">
      <label for="floatingTextarea2" class="form-label">Your comment:</label>
      <div class="form-floating">
        <textarea
          class="form-control"
          placeholder="Leave a comment here"
          id="floatingTextarea2"
          style="height: 100px"
          v-model="formData.comment"
        ></textarea>
        <label for="floatingTextarea2">Message:</label>
      </div>
    </div>
    <div class="col-12">
      <button type="submit" class="btn btn-primary">Send Message</button>
    </div>
  </form>
</template>

<script>
import { API } from "aws-amplify";
import { createTodo } from "../graphql/mutations";
import { listTodos } from "../graphql/queries";
export default {
  data() {
    return {
      formData: {
        name: "",
        email: "",
        phoneno: "",
        jobTitle: "",
        state: "",
        comment: "",
        fileUri: null,
      },
      todos: [],
    };
  },
  async created() {
    this.getTodos();
  },
  methods: {
    async submitForm() {
      console.log("Form data:", this.formData);
      const { name, email, phoneno, jobTitle, state, comment, fileUri } =
        this.formData;
      const todo = { name, email, phoneno, jobTitle, state, comment, fileUri };
      console.log(todo);
      try {
        await API.graphql({
          query: createTodo,
          variables: { input: todo },
        });
      } catch (error) {
        console.log(error);
      }
      this.formData.name = "";
      this.formData.email = "";
      this.formData.phoneno = "";
      this.formData.jobTitle = "";
      this.formData.state = "";
      this.formData.comment = "";
      this.formData.fileUri = null;
    },
    handleFileChange(event) {
      const selectedFile = event.target.files[0];
      this.formData.fileUri = selectedFile;
    },
    async getTodos() {
      const todos = await API.graphql({
        query: listTodos,
      });
      this.todos = todos.data.listTodos.items;
    },
  },
};
</script>

<style>
.btn-primary{
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
}
</style>
