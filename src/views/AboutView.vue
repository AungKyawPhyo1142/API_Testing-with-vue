<template>
  <div>

  </div>
</template>

<script>
import axios from "axios"
  export default {
    name: 'AboutView',
    mounted () {
        axios.get('http://localhost:3000/posts')
            .then(response => {
              console.log(response.data)
        })

    }
  }
</script>

<style lang="scss" scoped>

</style>