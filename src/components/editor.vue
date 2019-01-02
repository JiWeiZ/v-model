<template>
  <div>
    <tag-box :maxTagNum="3">新建一级标签（最多3个）</tag-box>
    <tag-box :maxTagNum="6">新建二级标签（最多6个）</tag-box>
  </div>
</template>

<script>
import tagBox from './tagBox'

export default {
  components: {
    tagBox
  }
}
</script>
