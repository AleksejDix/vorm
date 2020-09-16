<template>
  <label>
    <div>{{ $attrs.label }}</div>
    <input
      type="checkbox"
      :name="$attrs.label"
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
      type: Boolean,
      default: false,
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