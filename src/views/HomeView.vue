<template>
  <div class="home">
    <Menu></Menu>
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from '@/components/HelloWorld.vue'
import Menu from '@/components/Menu.vue'
export default{
  name: 'HomeView',
  components: {
    HelloWorld,
    Menu
  }
}
</script>


