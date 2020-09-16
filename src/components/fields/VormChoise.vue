<template>
  <div>
    <div>{{ $attrs.label }}</div>
    <label
      v-for="option in options"
      :key="option"
      class="block"
    >
      <input
        v-model="model"
        :type="$attrs.multiple ? 'checkbox' : 'radio'"
        :value="option"
      >
      <span>
        {{ option }}
      </span>
    </label>
  </div>
</template>

<script>
// layout? row col
// single multiple


export default {
  inheritAttrs: false,
  model: {
    prop: 'modelValue',
    event: 'update:modelValue'
  },
  props: {
    modelValue: {
      type: [String, Array],
      default: String
    },
    options: {
      type: Array,
      default: () => []
    }
  },
  computed: {
    model: {
      get() {
        if (!this.modelValue && this.$attrs.multiple)  return []
        if (!this.modelValue && !this.$attrs.multiple)  return ''
        return this.modelValue
      },
      set(value) {
        this.$emit('update:modelValue', value)
      }
    }
  }
}
</script>

<style scoped>
  .block {
    display: block
  }
</style>