<template>
  <ul class="todo-list">
    <!-- completed: 完成的类名 -->
    <li :class="{completed : item.isDone}" v-for="item in list" :key="item.id">
      <div class="view">
        <input class="toggle" type="checkbox" v-model="item.isDone"/>
        <label>{{item.name}}</label>
        <button class="destroy" @click="delTask(item.id)"></button>
      </div>
    </li>
  </ul>
  
</template>

<script>
export default {
  props:["list"],
  methods:{
    delTask(id){
      this.$emit('del-Task',id);
    }
  }
}
</script>