<template>
  <div class="todolist">
    <div style="margin-top: 15px;">
      <el-input type="text" 
        v-model="todo" 
        placeholder="edit me"
        @keyup.enter.native="addToDo">
        <template slot="append">
          <el-button type="success" icon="el-icon-check" circle @click="addToDo"></el-button>
        </template>
      </el-input>
      
      
    </div>
    
    <ul class="list">
      <li
        v-for="(item, index) in todoList"
        :key="index"
        @click="deleteTo(index)"
      >{{ item }}</li>
    </ul>
  </div>
</template>

<script>

export default {
  data() {
    return {
      todo: '',
      todoList: (localStorage.getItem("todolis") != null) ? eval(localStorage.getItem("todolis")) : [],
    }
  },
  methods: {
    addToDo() {
      this.todoList.push(this.todo);
      this.todo = '';
      localStorage.setItem("todolis", JSON.stringify(this.todoList));
      // console.log(this.todoList)
      
    },
    deleteTo(index) {
      // console.log('delete', index)
      this.todoList.splice(index,1);
      localStorage.setItem("todolis", JSON.stringify(this.todoList));
    }

  }
 
}
</script>
<style scoped>
.list {
  list-style: none; 
}
</style>
