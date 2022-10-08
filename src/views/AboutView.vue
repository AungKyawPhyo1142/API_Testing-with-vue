<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col border rounded p-3">
          <div class="input-group mb-3">
            <span class="input-group-text" id="inputGroup-sizing-default">Title</span>
            <input
              v-model="title"
              type="text"
              class="form-control"
              aria-label="Sizing example input"
              aria-describedby="inputGroup-sizing-default"
            />
          </div>
          <div class="input-group mb-3">
            <span class="input-group-text" id="inputGroup-sizing-default">Author</span>
            <input
              v-model="author"
              type="text"
              class="form-control"
              aria-label="Sizing example input"
              aria-describedby="inputGroup-sizing-default"
            />
          </div>
          <div class="input-group mb-3">
            <span class="input-group-text" id="inputGroup-sizing-default">Price</span>
            <input
              v-model="price"
              type="text"
              class="form-control"
              aria-label="Sizing example input"
              aria-describedby="inputGroup-sizing-default"
            />
          </div>
          <div class="px-2">
            <button class="btn btn-dark col-4" @click="addItems()">Add</button>
          </div>
        </div>
        <div class="col-7">
          <table class="table table-hover">
            <thead>
              <tr>
                <th scope="col">ID</th>
                <th scope="col">Title</th>
                <th scope="col">Author</th>
                <th scope="col">Price</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(item, index) in list" :key="index">
                <td scope="row">{{ item.id }}</td>
                <td scope="row">{{ item.title }}</td>
                <td scope="row">{{ item.author }}</td>
                <td scope="row">${{ item.price }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "AboutView",
  data() {
    return {
      list: [],
      title: '',
      price: '',
      author: '',
      itemCount: 0
    };
  },
  methods: {
    addItems () {
      let myData = {
        title: this.title,
        price: this.price,
        author: this.author,
        id: ++this.itemCount
      }
      axios.post('http://localhost:3000/posts',myData);
      this.loadData();
      this.clearForm();
    },
    loadData(){
      // get method
      axios.get("http://localhost:3000/posts").then((response) => {
        this.list = response.data;
        this.itemCount = response.data.length;
      });
    },
    clearForm(){
      this.title='',
      this.author='',
      this.price=''
    }
  },
  mounted() {
    this.loadData();
  },
};
</script>

<style lang="scss" scoped></style>
