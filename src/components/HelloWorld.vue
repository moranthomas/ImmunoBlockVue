<template>
  <div class="hello">
    <h1>{{ boundText }}</h1>
    <p>
      Welcome to the Global Autoimmune Tracking Repository<br>
      Created as part of the:
      <a href="https://gitcoin.co/issue/ConsenSys/Beyond-Blockchain-Relay/3/3158" target="_blank" rel="noopener">Beyond Blockchain Hackathon</a>.
    </p>
    <h3>Learn More</h3>
    <ul>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel" target="_blank" rel="noopener">About The Project</a></li>
      <li><a href="http://gitcoin.co/issue/ConsenSys/Beyond-Blockchain-Relay/3/3158" target="_blank" rel="noopener">About Gitcoin</a></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    boundText: String,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
