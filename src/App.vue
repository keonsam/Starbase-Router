<template>
  <div id="app">
    <h1 class="heading">Starbase Router</h1>
    <div id="nav">
      <router-link class="link" to="/characters"
        >Meet the Characters</router-link
      >
      |
      <router-link class="link" to="/planets">Explore the Planets</router-link>
    </div>
    <router-view />
  </div>
</template>

<style>
body {
  background: #263238;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
}

.link,
.link:hover,
.link:visited,
.link:active {
  color: #4fc08d;
}

.heading {
  margin-bottom: 50px;
}
</style>
