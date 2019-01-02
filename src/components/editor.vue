<template>
  <div>
    <tag-box :maxTagNum="6">新建一级标签（最多6个）</tag-box>
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
