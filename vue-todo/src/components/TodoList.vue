<template>
  <div>
    <ul>
      <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem.item" class="shadow">
        <i class="fas fa-check checkBtn" v-bind:class="{checkBtnCompleted:todoItem.completed}" v-on:click="toggleComplete(todoItem, index)"></i>
        <span v-bind:class="{textCompleted: todoItem.completed}">{{todoItem.item}}</span>
        <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
          <i class="fas fa-trash-alt"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default{
    props:['propsdata'],
    methods:{
    removeTodo : function(todoItem, index){
      this.$emit('removeItem', todoItem, index);
    },
    toggleComplete:function(todoItem, index) {
      todoItem.completed = !todoItem.completed;
      localStorage.removeItem(todoItem.irem);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    }
  }
}
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-left:0;
  margin-top:0;
  text-align: left;
}
li{
  display: flex;
  min-height: 50px;
  height:50px;
  line-height: 50px;
  margin:.5rem 0;
  padding: 0 .9rem;
  background:white;
  border-radius: 5px;
}
.checkBtn {
  line-height: 45px;
  color:#62acde;
  margin-right: 5px;
}
.checkBtnCompleted {
  color:#d3adad;
}
.textCompleted{
  text-decoration: line-through;
  color:#b3adad;
}
.removeBtn{
  margin-left:auto;
  color:#de4343;
}
</style>