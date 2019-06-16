<template>
  <div id="app">
    <header>
      <nav>
        <ul>
          <li class="nav-item">
            <router-link class="nav-link" to="/" exact>
            <img class="logo" alt="Vue logo" src="./assets/build-a-bot-logo.png">
              Home
            </router-link>
          </li>
           
          <li class="nav-item">
            <router-link class="nav-link" to="/build" exact>Build Robot</router-link>
           </li> 

        </ul>

      </nav>
    </header>
    <main>
      <!-- <HomePage msg="Welcome to the World of Bot"/> -->
      <!-- <RobotBuilder/> -->
      <router-view></router-view>
    </main>
  </div>
</template>

<script>
//  import HomePage from './Home/HomePage.vue';
// import RobotBuilder from "./build/RobotBuilder.vue";

export default {
  name: "app",
  // components: {
  //   RobotBuilder
  // }
};
</script>

<style>
body {
  background-color: #485460;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
main {
  margin: 0 auto;
  background-color: white;
  padding: 30px;
  width: 1024px;
  min-height: 300px;
}
header {
  background-color: #808e9b;
  width: 1084px;
  margin: 0 auto;
  border-radius: 7px;
}
ul {
  padding: 3px;
  display: flex;
}
.nav-item {
  display: inline-block;
  padding: 5px 10px;
  font-size: 22px;
  border-right: 1px solid #bbb;
}
.logo {
  vertical-align: middle;
  height: 30px;
}
.nav-link{
  text-decoration:none;
  color:inherit;
}
.router-link-active{
  color:white;
}
</style>
