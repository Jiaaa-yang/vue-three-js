<template>
  <header id="navbar">
    <ul>
      <li><a href="" @click.prevent="showVue">VueJs</a></li>
      <li><a href="" @click.prevent="showThree">ThreeJS</a></li>
    </ul>
  </header>
  <div id="content">
    <!-- Demonstration of VueJS functionalities -->
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
    <!-- Demonstration of ThreeJS functionalities -->
    <div v-show="threeDemo">
      <h1>This is created using ThreeJS!</h1> 
      <div>
        <select v-model="geometry">
          <option disabled value="">Geometry Type</option>
          <option>Box</option>
          <option>Sphere</option>
        </select>
      </div>
      <!-- ThreeJS components imported using 'troisjs' library -->
      <Renderer width=650 height=650 :orbitCtrl=true>
        <Camera :position="{z: 10}"/>
        <Scene background="#150050">
          <PointLight :position="{x: 4, y: 5, z: 5}" />
          <Mesh>
            <BoxGeometry v-if="showBox" :width=width :height=height :depth=depth />
            <SphereGeometry v-if="showSphere" :radius=radius :widthSegments=64 :heightSegments=64 />
            <StandardMaterial color="#bfd8b8"/>
          </Mesh>
        </Scene> 
      </Renderer>
      <div v-show="showBox" id="box-dimensions">
        <span>Height</span><Slider v-model="height" :min=1 :max=5 />
        <span>Width</span><Slider v-model="width" :min=1 :max=5 />
        <span>Depth</span><Slider v-model="depth" :min=1 :max=5 />
      </div>
      <div v-show="showSphere" id="box-dimensions">
        <span>Radius</span><Slider v-model="radius" :min=1 :max=3 />
      </div>
    </div>
  </div>
</template>

<script>
import { Renderer, Scene, Camera, BoxGeometry, Mesh, StandardMaterial, PointLight, SphereGeometry } from 'troisjs';
import Slider from '@vueform/slider'

export default {
  name: 'App',
  components: { Renderer, Scene, Camera, BoxGeometry, Mesh, StandardMaterial, PointLight, SphereGeometry, Slider },
  data() {
    return {
      vueDemo: true,
      threeDemo: false,
      count: 0,
      message: "",
      todo: "",
      todos: [],
      width: 2,
      height: 2,
      depth: 2,
      radius: 1,
      geometry: ""
    }
  },
  computed: {
    showBox() {
      return this.geometry == 'Box'
    },
    showSphere() {
      return this.geometry == 'Sphere'
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

<style src="@vueform/slider/themes/default.css"></style>
<style>
/* General */
body {
  background-color: lavender;
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

select {
  margin: 1%;
}

/* Default styling for app */
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

/* Navbar */
#navbar li {
  padding: 0 3rem;
  display: inline;
}

#navbar a {
  font-size: 1.5rem;
  text-decoration: none;
}

/* Content */
.container {
  background-color: #ffb6c1;
  padding: 4%;
  margin: 2% 6%;
  border-radius: 6px;
  font-size: 1.5rem;
}

#box-dimensions {
  margin: auto;
  margin-top: 2%;
  margin-bottom: 2%;
  width: 30%;
}

#box-dimensions span {
  margin: 5%;
}
</style>
