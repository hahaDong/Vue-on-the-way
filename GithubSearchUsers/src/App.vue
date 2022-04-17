<template>
    <div class="container">
      <h1>GitHub Search users</h1>
      <Search/>
      <List/>
    </div>
</template>

<script>
  import Search from "./components/Search.vue"
  import List from "./components/List.vue"

  export default {
    name: 'App',
    components: {
      Search,
      List
    }
  }
</script>

<style>
  h1{
    text-align: center;
  }
</style>
