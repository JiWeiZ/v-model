<template>
  <div class="tag-box">
    <div
      v-for="(item, index) in tagInputs"
      :key="item.id"
      :is="item.component"
      v-model="item.value"
      @keydown.enter.native="onAddTag"
      @deleteTag="onDeleteTag(index)"
      @focusPrevious="onFocusPrevious(index)"
    ></div>
    <div v-if="this.tagInputs.length < this.maxTagNum" class="tag-title" @click="onAddTag">
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
    maxTagNum: {type: Number, default: 5}
  },
  data () {
    return {
      tagInputs: []
    }
  },
  methods: {
    onAddTag () {
      if (this.tagInputs.length) {
        if (this.tagInputs.length >= this.maxTagNum) return
        for (let item of this.tagInputs) {
          if (item.value === '') return
        }
      }
      this.tagInputs.push({
        component: tagInput,
        value: '',
        id: Date.now()
      })
    },
    onDeleteTag (index) {
      if (this.tagInputs.length) {
        this.tagInputs.splice(index, 1)
      }
    },
    onFocusPrevious (index) {
      if (index !== 0) {
        this.$el.children[index - 1].children[0].focus()
      }
    }
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
