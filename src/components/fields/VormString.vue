<template>
  <label>
    <div>{{ $attrs.label }}</div>
    <input
      type="text"
      v-model="model"
      v-bind="$attrs"
    >
  </label>
</template>

<script>
export default {
  inheritAttrs: false,
  model: {
    prop: 'modelValue',
    event: 'update:modelValue'
  },
  props: {
    modelValue: {
      type: String,
      default: '',
    }
  },
  computed: {
    model: {
      get() {
        return this.modelValue
      },
      set(value) {
        this.$emit('update:modelValue', value)
      }
    }
  }
}
</script>