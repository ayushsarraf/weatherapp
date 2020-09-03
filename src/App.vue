<template>
  <div id="app">
    <Search></Search>
    <Result></Result>
  </div>
</template>

<script>
import Search from './components/Search'
import Result from './components/Result'
export default {
  name: 'App',
  components: {
    Search:Search,
    Result:Result
  }
}
</script>

<style>
body{

  background-color: black;
}
#app{
  height: 100%;
}
</style>
