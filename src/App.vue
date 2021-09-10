<template>
  <header id="navbar">
    <ul>
      <li><a href="" @click.prevent="showVue">VueJs</a></li>
      <li><a href="" @click.prevent="showThree">ThreeJS</a></li>
    </ul>
  </header>
  <div id="content">
    <div v-show="vueDemo">
      <h1>These are some functionalities implemented with Vue!</h1>
      <div class="container">
        <span>Click counter: {{ count }}</span><button id="clickerButton" @click="addCount">Add Count</button>
      </div>
      <div class="container">
        <h3>Input Tracker</h3>
        <p>Your input is: {{message}}</p>
        <input v-model="message" type="text">
      </div>
      <div class="container">
        <h3>TODO List</h3>
        <ol>
          <li v-for="todo in todos" :key="todo">{{ todo }}</li>
        </ol>
        <input type="text" v-model="todo">
        <button @click="addTodo">Add Task</button>
      </div>
    </div>
    <div v-show="threeDemo">
      <Renderer>
      <Camera :position="{ z: 50 }" />
      <Scene>
        <PointLight :position="{ y: 50, z: 50 }" />
        <Box>
          <LambertMaterial />
        </Box>
      </Scene>
      </Renderer>
    </div>
  </div>
</template>

<script>
import { Box, Camera, LambertMaterial, PointLight, Renderer, Scene } from 'troisjs';
export default {
  name: 'App',
  components: { Box, Camera, LambertMaterial, PointLight, Renderer, Scene },
  data() {
    return {
      vueDemo: true,
      threeDemo: false,
      count: 0,
      message: "",
      todo: "",
      todos: [],
    }
  },
  methods: {
    addCount() {
      this.count++;
    },
    addTodo() {
      if (this.todo) {
        this.todos.push(this.todo)
      }
    },
    showVue() {
      this.vueDemo = true
      this.threeDemo = false
    },
    showThree() {
      this.threeDemo = true
      this.vueDemo = false
    }
  }
}
</script>

<style>
body {
  background-color: lavender;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#navbar li {
  padding: 0 3rem;
  display: inline;
}

#navbar a {
  font-size: 1.5rem;
  text-decoration: none;
}

.container {
  background-color: #ffb6c1;
  padding: 4%;
  margin: 2% 6%;
  border-radius: 6px;
  font-size: 1.5rem;
}

button {
  display: inline;
  background-color: cadetblue;
  color: white;
  border: none;
  margin: 1% 3%;
  padding: 0.5rem;
  cursor: pointer;
}

ol {
  text-align: start;
  width: 30%;
  margin: auto;
}
</style>
