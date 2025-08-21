<template>
  <div>
    <input
      placeholder="What needs to be done?"
      class="input"
      v-model="newTask"
      @keyup.enter="addTask"
    />
    <div v-if="tasks.length">

    <div v-for="(task, index) in tasks" :key="task.id" class="task">
      <div class="taskItemLeft">
        <input type="checkbox" class="checkbox" v-model="task.completed">
         <!-- Apply completed class if todo.completed is true -->
        <p v-if="!task.edited" @dblclick="editTask(task)" class="tasktitle" :class="{completed: task.completed}">
          {{ task.title }}
        </p>
        <input
          v-else
          type="text"
          class="taskInput"
          v-model="task.title"
          @blur="doneEditing(task)"
          @keyup.enter="doneEditing(task)"
          @keyup.esc="cancelEditing(task)"
          v-focus
        />
      </div>
      <div class="close-btn" :class="{completeClose: task.completed}" @click="removeTask(index)">&times;</div>
    </div>
    </div>
    <div  v-if="tasks.length" class="extra-container">
      <div><label style="color:#fff"><input type="checkbox" class="checkbox" :checked="!anyRemaining" @change="checkAll"/>Check All</label></div>
      <div>
        <p v-if="remaining > 1">{{remaining}} Tasks remaining</p>
        <p v-else-if="remaining == 1" >{{remaining}} Task remaining</p>
        <p v-else >Good Job!👏 <span class="block"> All tasks completed. </span></p>
       
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "todo-list",
  data() {
    return {
      newTask: "",
      idForTask: 1,
      beforeEditCache: "",
      tasks: [
        // {
        //   id: 1,
        //   title: "Build the basics of a task app",
        //   completed: false,
        //   edited: false,
        // },
        // {
        //   id: 2,
        //   title: "Go to Koforidua",
        //   completed: false,
        //   edited: false,
        // },
      ],
     
    };
  },
  computed:{
   remaining (){
    return this.tasks.filter(task => !task.completed).length
   } ,
   anyRemaining (){
    return this.remaining != 0
   }
  },
  directives: {
    focus: {
      mounted: function (el) {
        el.focus();
      },
    },
  },
  methods: {
    addTask() {
      if (this.newTask.trim().length == 0) {
        return;
      }
      this.tasks.push({
        id: this.idForTask,
        title: this.newTask,
        completed: false,
        edited: false,
      });
      this.newTask = "";
      this.idForTask += 1;
    },
    editTask(task) {
      this.beforeEditCache = task.title;
      task.edited = true;
    },
    doneEditing(task) {
      if (task.title.trim().length == 0) {
        task.title = this.beforeEditCache;
      }
      task.edited = false;
    },
    cancelEditing(task) {
      task.title = this.beforeEditCache;
      task.edited = false;
    },
    removeTask(index) {
      alert(
        "Are you sure you want to delete this task?",
        this.tasks.splice(index, 1)
      );
    },
    checkAll(){
      this.tasks.forEach((task) => task.completed = event.target.checked )
    },
  },
  watch: {
    remaining(newVal) {
      // when remaining tasks hit 0
      if (newVal === 0 && this.tasks.length > 0) {
        alert("Only if Life was Need For Speed.\nTry again tomorrow and you might turn your dreams into reality.");
      }
    }
  },
};
</script>

<style >
.input {
  width: 100%;
  padding: 10px 18px;
  font-size: 18px;
  margin-bottom: 15px;
  border-radius: 16px;
  border: 1px lightgrey solid;
  color: #2c3e50;
  
}
.input:focus {
  border: 1px grey solid;
  outline: none;
}

.tasktitle {
  font-size: 18px;
  color: #fff;
}

.task {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.taskItemLeft {
  display: flex;
  align-items: center;
}
.close-btn {
  font-size: 20px;
  cursor: pointer;
  color: red;
}
.taskInput {
  padding: 8px 16px;
  border-radius: 7px;
  border: 1px solid gray;
  font-size: 18px;
  color: #2c3e50;
}
.taskInput:focus {
  outline: none;
}

.close-btn:hover {
  color: rgba(255, 0, 0, 0.515);
}

.checkbox{
  margin-right: 10px;
  cursor: pointer;
  
}
.extra-container{
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 14px;
  border-top: 1px solid lightgrey;
  padding: 8px 0;
  cursor: pointer;
}
.completed{
  text-decoration: line-through;
  color: #fff;
}

.completeClose{
  color: rgba(255, 0, 0, 0.311);
}
.block{
  display: block;
}

</style>