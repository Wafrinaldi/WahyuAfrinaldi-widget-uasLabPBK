<template>
  <div id="app">
    <header>
      <nav>
        <ul>
          <li><router-link to="/">Weather</router-link></li>
          <li><router-link to="/location">Location</router-link></li>
          <li><router-link to="/stopwatch">Stopwatch</router-link></li>
          <li><router-link to="/Game">Game</router-link></li>
          <li><router-link to="/photo">Photo</router-link></li>
        </ul>
      </nav>
    </header>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style>
#app {
  text-align: center;
  font-family: 'Poppins', sans-serif;
}

header {
  background: #fa8072;
  padding: 20px;
}

nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

nav li {
  display: inline-block;
  margin-right: 15px;
}

nav a {
  color: #fff;
  text-decoration: none;
  padding: 15px 20px;
  font-size: 20px;
  font-weight: 500;
}

nav a:hover {
  font-size: 22px;
  transition: all 1s;
  border-radius: 5px;
}
</style>
