<template lang="pug">
.container
  h1 Todo app with VUE
  .items(v-for="items in todos" :id="items.id")
    input(type="checkbox" v-model="items.checked")
    span(:class="{checked: items.checked}" class="content") {{items.task}}
    button(@click="deleteItem(items.id)") deleteItem
  .input
    input(type="text" v-model="newTodo")
    button(@click="addItem") addItem
  p(v-if="warning.length>0") {{warning}}
</template>

<script>
export default {
  data(){
    return{
      id:1,
      newTodo:"",
      todos:[{task:"Hello",id:1,checked:false}],
      warning : ""
    }
  },
  methods : {
    addItem(){
      if (this.newTodo.length==0){
        this.warning= "invalid Input"
        return;
      }
      this.warning = ""
      this.todos.push({task:this.newTodo,id:this.id,checked:false});
      this.id+=1;
      this.newTodo = ""
    },
    deleteItem(id){
      this.todos = this.todos.filter((item)=>item.id!==id)
    }
  }
}
</script>

<style>
html{
  height:100%;
}
body{
  height:100%;
}
.checked{
  text-decoration: line-through;
}
.container{
  width:fit-content;
  position: relative;
  left:50%;
  top:50%;
  transform: translate(-50%,-50%);
}
.items{
  margin: 10px;
  display: flex;
  justify-content: space-around;
}
.content{
  flex-grow: 1;
}
.input{
  display: flex;
  justify-content: space-around;
}


</style>