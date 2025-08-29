<template >
  <div class="appWrapper">
    <transition name="fade">
      <div
        :key="backgroundImage"
        class="background"
        :style="{
          backgroundImage: `url(${backgroundImage})`,
          backgroundSize: 'cover',
          backgroundPosition: '50% 70%',
          backgroundRepeat: 'no-repeat',
        }"
      ></div>
    </transition>
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
      currentBg: "",
      intervalId: null,
      isFading: false,
      currentIndex: 0,
      bg: [
        [
          "https://images.unsplash.com/photo-1616455263449-0bd3aac04029?q=80&w=687&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
          "https://images.unsplash.com/photo-1754004958928-4175eadc3d33?q=80&w=687&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
          "https://images.unsplash.com/photo-1739161763843-4adaf7709291?q=80&w=687&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
          "https://images.unsplash.com/photo-1657769207339-562f3d9207a8?q=80&w=687&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
          "https://images.pexels.com/photos/6005257/pexels-photo-6005257.jpeg",
          "https://images.unsplash.com/photo-1748269169676-ea2872d947d6?q=80&w=765&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
        ],
        [
          "https://images.unsplash.com/photo-1583917070471-e6e2022a31af?q=80&w=687&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
          "https://images.pexels.com/photos/6005257/pexels-photo-6005257.jpeg",
          "https://images.unsplash.com/photo-1749599356476-96da9d36a4c0?w=600&auto=format&fit=crop&q=60&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1yZWxhdGVkfDEyfHx8ZW58MHx8fHx8",
          "https://images.unsplash.com/photo-1629450646257-87251b691036?q=80&w=764&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
          "https://images.unsplash.com/photo-1660139131278-607310e532fe?q=80&w=1169&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
          "https://images.unsplash.com/photo-1632823469328-3e4032015d78?q=80&w=1170&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
          "https://images.unsplash.com/photo-1680446983373-853872fb667a?q=80&w=1170&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
        ],
      ],
    };
  },
  computed: {
    backgroundImage() {
      return this.currentBg;
    },
  },
  methods: {
    handleAnswered(option) {
      this.selectedCar = option;
      this.answered = true;
      this.currentBg;
      this.setChangeBg(option);

      // if (this.intervalId) {
      //   clearInterval(this.intervalId);
      // }

      // Start changing background every 6 seconds
      this.intervalId = setInterval(() => {
        this.setChangeBg(option);
      }, 10000);
    },
    setChangeBg(option) {
      let index = option === "bmw" ? 0 : 1;
      let images = this.bg[index];

      this.currentBg = images[this.currentIndex];
      this.currentIndex = (this.currentIndex + 1) % images.length;
      // console.log("curnt ",this.currentBg)
    },
  },
  beforeUnmount() {
    if (this.intervalId) {
      clearInterval(this.intervalId);
    }
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
  position: relative;
  min-height: 100vh;
  width: 100%;
}

.background {
  position: absolute;
  inset: 0;
  z-index: -1;
  /* transition: opacity 0.8s ease-in-out; */
}

/* Fade transition classes */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 1.5s ease-in-out;
  position: absolute;
  inset: 0;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.appWrapper::before {
  content: "";
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.4); /* adjust opacity (0.3 = 30% darker) */
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

@media (max-width: 768px) {
  .container {
    max-width: 400px;
  }
  .components {
    padding-top: 6rem;
  }
}
@media (max-width: 540px) {
  .container {
    max-width: 300px; /*Width shouldn't be more than 600px*/
  }
}
</style>
