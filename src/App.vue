<template >
  <div
    class="appWrapper"
    :style="{
      backgroundImage: backgroundImage
        ? 'url(' + backgroundImage + ')'
        : 'none',
      backgroundRepeat: 'no-repeat',
      backgroundPosition: '50% 70%',
      backgroundSize: 'cover',
    }"
  >
    <div class="container">
      <div class="components">
        <img alt="Vue logo" src="./assets/logo.png" class="logo" />

        <QuestionComp v-if="!answered" @answered="handleAnswered" />
        <todo-list v-else></todo-list>
      </div>
    </div>
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";
import QuestionComp from "./components/Question.vue";

export default {
  name: "App",
  components: {
    TodoList,
    QuestionComp,
  },
  data() {
    return {
      answered: false,
      selectedCar: null,
      bg: [
        "https://images.unsplash.com/photo-1616455263449-0bd3aac04029?q=80&w=687&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
        "https://images.unsplash.com/photo-1583917070471-e6e2022a31af?q=80&w=687&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
      ],
    };
  },
  computed: {
    backgroundImage() {
      if (this.selectedCar === "bmw") {
        return this.bg[0];
      } else if (this.selectedCar === "benz") {
        return this.bg[1];
      }
      return ""; // default
    },
  },
  methods: {
    handleAnswered(option) {
      this.selectedCar = option;
      this.answered = true;
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  color: #ccc;
}
html,
body {
  padding: 0;
  margin: 0;

}

body {
  background: #20232a;
}
.container {
  max-width: 600px; /*Width shouldn't be more than 600px*/
  margin: 0 auto; /*center content in the div*/
  position: relative;
  z-index: 1;
}
.components {
  padding-top: 4rem;
}

.appWrapper {
  height: 100vh;
  width: 100vw;
  position: relative;
}
.appWrapper::before {
  content: "";
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.3); /* adjust opacity (0.3 = 30% darker) */
  z-index: 0;
}
.logo {
  display: block; /*no text should be beside it*/
  margin: 0 auto;
  height: 45px;
  padding-bottom: 0.5rem;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
}

@media (max-width: 768px){
  .container {
  max-width: 400px; 
}
.components {
  padding-top: 6rem;
}
}
@media (max-width: 540px){
  .container {
  max-width: 300px; /*Width shouldn't be more than 600px*/
}
}
</style>
