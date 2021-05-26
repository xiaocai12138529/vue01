<template>
  <footer class="footer">
    <span class="todo-count"
      >剩余<strong>{{ list.length }}</strong></span
    >
    <ul class="filters">
      <li>
        <a
          :class="{ selected: listStatus === 'all' }"
          href="javascript:;"
          @click="changeStatus('all')"
          >全部</a
        >
      </li>
      <li>
        <a
          :class="{ selected: listStatus === 'unOk' }"
          href="javascript:;"
          @click="changeStatus('unOk')"
          >未完成</a
        >
      </li>
      <li>
        <a
          :class="{ selected: listStatus === 'ok' }"
          href="javascript:;"
          @click="changeStatus('ok')"
          >已完成</a
        >
      </li>
    </ul>
    <button class="clear-completed" @click="$emit('del-ok')">清除已完成</button>
  </footer>
</template>

<script>
export default {
  props: ["list", 'listStatus'],
  methods: {
    changeStatus (status) {
      console.log(status)
      this.$emit('change-status', status)
    },
    // 删除已完成的数据
    
  }

}
</script>