<template>
  <div class="todoapp">
    <Head :list="list" @add-Task="addTask" />
    <Main :list="newList" @del-Task="delTask" />
    <Foot
      :list="list"
      :listStatus="listStatus"
      @change-status="changeStatus"
      @del-ok="delOkTask"
    />
  </div>
</template>

<script>
/**
 * 根据不同的任务状态切换列表数据
 * 思路:
 * 1.明确几个切换转态=> 全部 未完成 已完成
 * 2.点击的时候根据这三个状态切换数据,同时显示高亮状态
 */
import Head from './views/head'
import Main from './views/main'
import Foot from './views/foot'

export default {
  data () {
    return {
      // 任务列表的转态 => 全部('all') 未完成(unOk) 已完成(ok)
      listStatus: "all",
      // 任务列表数据
      list: JSON.parse(localStorage.getItem('list-task')) || []
      // [
      //   { id: 100, name: "吃饭", isDone: true },
      //   { id: 201, name: "睡觉", isDone: false },
      //   { id: 103, name: "打豆豆", isDone: true },
      // ],
    }
  },
  components: {
    Head,
    Main,
    Foot
  },
  methods: {
    // 添加任务  子组件通知我添加任务
    addTask (name) {
      this.list.push({
        name,
        id: Date.now(),
        isDone: false
      })
    },
    delTask (id) {
      this.list = this.list.filter((item) => item.id !== id)
    },
    changeStatus (status) {
      this.listStatus = status
    },
    // 删除功能
    delOkTask () {
      console.log(123)
      this.list = this.list.filter(item => !item.isDone)
    }
  },
  // 计算属性: 根据listStatus的转态计算当前的列表最新数据
  computed: {
    newList () {
      if (this.listStatus === 'unOk') {
        return this.list.filter(item => !item.isDone)
      } else if (this.listStatus === 'ok') {
        return this.list.filter(item => item.isDone)
      } else {
        return this.list
      }
    },
   
  },
  // 监控数据然后存储数据
  watch: {
    list: {
      deep: true,
      handler () {
        localStorage.setItem('list-task', JSON.stringify(this.list))
      }
    }
  }

}
</script>

<style>
</style>
