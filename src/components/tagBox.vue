<template>
  <div class="tag-box">
    <tag-input
      v-for="(item, index) in tags"
      :key="index"
      v-model="tags[index]"
      @keydown.enter.native="onAddTag"
      @deleteTag="onDeleteTag(index)"
      @focusPrevious="onFocusPrevious(index)"
    ></tag-input>
    <div v-if="this.tags.length < this.maxTagNum" class="tag-title" @click="onAddTag">
      <i class="fas fa-plus-square"></i><span class="tag-title-content"><slot></slot></span>
    </div>
  </div>
</template>

<script>
import tagInput from './tagInput'

export default {
  components: {
    tagInput
  },
  props: {
    maxTagNum: {type: Number, default: 5},
    initTags: {type: Array, default: () => []}
  },
  model: {
    prop: 'initTags',
    event: 'tagsChange'
  },
  data () {
    return {
      tags: []
    }
  },
  methods: {
    onAddTag () {
      if (this.tags.length) {
        if (this.tags.length >= this.maxTagNum) return
        for (let item of this.tags) {
          if (item.value === '') return
        }
      }
      this.tags.push('')
    },
    onDeleteTag (index) {
      if (this.tags.length) {
        this.tags.splice(index, 1)
      }
    },
    onFocusPrevious (index) {
      if (index !== 0) {
        this.$el.children[index - 1].children[0].focus()
      }
    }
  },
  watch: {
    tags () {
      this.$emit('tagsChange', this.tags)
    }
  },
  created () {
    this.tags = this.initTags
  }
}
</script>

<style scoped>
.tag-box {
  margin: 0 auto;
  min-height: 26px;
}

.tag-input {
  font-size: 14px;
  padding: 5px;
  width: 12em;
  outline: none;
  border: none;
}
.tag-title-content {
  margin-left: 5px;
}
.tag-title {
  display: inline-block;
  margin: 5px;
  color: #2790da;
}
.tag-title:hover {
  cursor: pointer;
}
</style>
