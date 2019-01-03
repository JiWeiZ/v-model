<template>
  <div>
    <tag-box :maxTagNum="3">新建一级标签（最多3个）</tag-box>
    <tag-box :maxTagNum="6">新建二级标签（最多6个）</tag-box>
    <mul-input></mul-input>
  </div>
</template>

<script>
import tagBox from './tagBox'
import mulInput from './mulInput'

export default {
  components: {
    tagBox,
    mulInput
  },
  data () {
    return {
      tags1: []
    }
  }
}
</script>
