<template>
  <div>
    <tag-box v-model="tags1" :maxTagNum="3">新建一级标签（最多3个）</tag-box>
    <tag-box v-model="tags2" :maxTagNum="6">新建二级标签（最多6个）</tag-box>
  </div>
</template>

<script>
import tagBox from './tagBox'

export default {
  components: {
    tagBox
  },
  data () {
    return {
      tags1: [],
      tags2: [5, 6, 7]
    }
  }
}
</script>
