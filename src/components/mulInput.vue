<template>
  <div class="mul-input">
    <div>
      <button @click="arr.push(1)">增加</button>
      <button @click="arr.pop()">删除</button>
    </div>
    <input type="text"
      v-for="(item, index) in arr"
      :key="index"
      v-model="arr[index]"
      >
  </div>
</template>

<script>
export default {
  data () {
    return {
      arr: []
    }
  }
}
</script>
