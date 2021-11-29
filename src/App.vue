<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
// const electron = window.require('electron');

// export default {
//   mounted: function() {
//     electron.ipcRenderer.on('goToHome', () => {
//       this.$router.push('/');
//     });
//     electron.ipcRenderer.on('goToAbout', () => {
//       this.$router.push('/about');
//     });
//   },
// };
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
