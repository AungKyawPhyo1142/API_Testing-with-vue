<template>
  <div>

    <h1 class="text-dark">API Testing with Fake Store API</h1>
    <button class="mt-2 btn btn-dark text-white" @click="getData()">Get Data</button>

    <div class="row mt-4">
      <table class="table table-hover">
        <thead>
          <tr>
            <th scope="col">ID</th>
            <th scope="col">Image</th>
            <th scope="col">Title</th>
            <th scope="col">Price</th>
            <th scope="col">Category</th>
          </tr>
        </thead>
        <tbody>
          <tr v-if="items.length==0">
            <td colspan="5" scope="row">There are no data at the moment</td>
          </tr>
          <tr v-else v-for="(item,index) in items" :key="index">
            <td scope="row">{{item.id}}</td>
            <td scope="row"><img :src="item.image" width="100" alt="" class="img-thumbnail"></td>
            <td scope="row">{{item.title}}</td>
            <td scope="row">${{item.price}}</td>
            <td scope="row">{{item.category}}</td>
          </tr>
        </tbody>
      </table>
    </div>

  </div>
</template>

<script>
  export default {
    name: 'HomeView',
    data () {
      return {
        loadingStatus: false,
        items: []
      }
    },
    methods: {
      getData () {
        this.loadingStatus=true;
        fetch('https://fakestoreapi.com/products')
            .then(res=>res.json())
            .then(json=>
              {
                this.items = json;
                this.loadingStatus=false;
              }
            )  
     
      }
    }
  }
</script>