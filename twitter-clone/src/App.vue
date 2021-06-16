<template>
  <div>
    <nav>
      <router-link to="/">
        <div id="logo">Twitter</div>
      </router-link>
    </nav>
    <router-view />
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0;
}

nav {
  padding: 10px 30px;
  margin: 0 0 10px 0;
  background: rgb(142, 181, 224);
  height: 40px;
  width: 100%;
  text-align: left;
  font-size: 1.6rem;
  font-weight: bolder;
  display: flex;
}

a {
  color: inherit;
  text-decoration: none;
}
</style>
