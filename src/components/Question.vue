<template>
  <div class="questionWrapper">
    <p class="question">Which one of these is your dream car?</p>

    <div class="answer">
      <label class="">
        <input type="radio" value="bmw" v-model="selectedOption" />BMW
      </label>
    
      <label>
        <input type="radio" value="benz" v-model="selectedOption" />Benz
      </label>
    </div>
    <div class="flex">
      <button class="send" @click="send" @keyup.enter="send" :disabled="!selectedOption">Send</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "QuestionComp",
  data() {
    return {
      selectedOption: "",
    };
  },
  methods:{
    send(){
      this.$emit("answered", this.selectedOption)
    }
  },
};
</script>

<style scoped>
.question {
  font-size: 20px;
  font-display: 500px;
}

@media (max-width: 540px){
  .question {
  font-size: 17px;
  font-display: 600px;
}
}
.questionWrapper{
  display: grid;
  place-items: center;
  height: 100%;


}
.answer {
    display: flex;
    flex-direction: column;
  font-size: 18px;
  margin-bottom: 12px;
}
input{
    margin: 0px 10px 10px 0px;
}


.send {
  padding: 4px 20px;
  font-size: 1rem;
  background: #41b883;
  color: #fff;
  border-radius: 8px;
  cursor: pointer;
}
/* .flex {
  display: flex;
  justify-content: right;
} */
</style>