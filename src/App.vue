<template>
    <div>
        <Navbar/>
        <router-view/>
    </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
export default {
    components: {Navbar}
}
</script>

<style>
body {
  background: #f2f2f2;
}
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: left;
    max-width: 600px;
    margin: 0 auto;
    color: #2c3e50;
}
</style>
