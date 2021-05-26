<template>
  <header class="header">
    <h1>todos</h1>
    <input
      id="toggle-all"
      class="toggle-all"
      type="checkbox"
      v-model="allStatus"
    />
    <label for="toggle-all"></label>
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      @keyup.enter="addTask"
      v-model="name"
    />
  </header>
</template>

<script>
export default {
  props: ["list"],
  computed: {
    allStatus: {
      get () {
        return this.list.every(item => item.isDone)
      },
      set (val) {
        this.list.forEach(item => item.isDone = val)
      }
    }
  },
  data () {
    return {
      name: ''
    }
  },
  methods: {
    // 回车添加新任务
    addTask () {
      /**
       * 1.校验输入 非空 
       * 2.校验通知父组件添加新任务
       *  */
      if (!this.name) {
        return alert('输入不能为空')
      }
      this.$emit('add-Task', this.name)
      this.name = ''
    },

  },

}
</script>