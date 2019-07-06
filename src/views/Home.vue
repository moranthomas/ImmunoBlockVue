<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/consensys_logo.png">
    <HelloWorld :boundText="parentMessage"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  components: {
    HelloWorld
  },
  data() {
    return {
      parentMessage: 'Autoimmune Disease Registry'
    }
  }
}
</script>
