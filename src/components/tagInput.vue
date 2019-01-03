<template>
  <div class="tag-input-wrapper">
    <input
      type="text"
      class="tag-input"
      :style="{width: inputWidth + 'em'}"
      maxlength="20"
      :value="tagValue"
      v-bind="$attrs"
      v-on="inputListeners"
      v-focus
    ><span class="tag-input-icon"><i class="fas fa-times" @click="emitDeleteTag"></i></span>
  </div>
</template>

<script>
export default {
  directives: {
    focus: {
      inserted (el) {
        el.focus()
      }
    }
  },
  model: {
    prop: 'tagValue'
  },
  props: {
    tagValue: [String, Number]
  },
  data () {
    return {
      readyToDelete: false,
      inputWidth: 1
    }
  },
  computed: {
    inputListeners () {
      let vm = this
      return Object.assign({}, this.$listeners, {
        input (e) {
          vm.$emit('input', e.target.value)
        },
        blur () {
          if (vm.tagValue === '') vm.emitDeleteTag()
        },
        keydown (e) {
          if ((e.keyCode === 8 || e.keyCode === 46) && vm.tagValue === '') {
            vm.readyToDelete = true
          }
        },
        keyup (e) {
          if ((e.keyCode === 8 || e.keyCode === 46) &&
          vm.tagValue === '' &&
          vm.readyToDelete) {
            vm.emitDeleteTag()
            vm.$emit('focusPrevious')
            vm.readyToDelete = false
          }
        }
      })
    }
  },
  methods: {
    emitDeleteTag () {
      this.$emit('deleteTag')
    }
  },
  watch: {
    tagValue () {
      // 考虑中英文字符宽度不同
      let tagValue = this.tagValue
      if (tagValue && tagValue.length) {
        let reLen = 0
        for (let i = 0; i < tagValue.length; i++) {
          if (tagValue.charCodeAt(i) >= 0 && tagValue.charCodeAt(i) <= 128) {
            reLen += 0.5
          } else {
            reLen += 1
          }
        }
        this.inputWidth = (reLen + 1)
      } else {
        this.inputWidth = 1
      }
    }
  }
}
</script>

<style scoped>
.tag-input-wrapper {
  display: inline-block;
  margin: 5px;
}
.tag-input {
  border: none;
  background: #addaf9;
  color: #222;
  outline: none;
  border-radius: 3px;
  padding: 3px 5px;
  min-width: 1.5em;
  font-size: 13px;
  font-family: Consolas, monospace;
}
.tag-input-icon {
  color: #2790da;
  margin-left: 5px;
}
.tag-input-icon:hover{
  cursor: pointer;
}
</style>
