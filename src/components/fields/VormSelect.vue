<template>
  <label>
    <div>{{ $attrs.label }}</div>
    <select
      name="$attrs.label"
      v-model="model"
      :multiple="$attrs.multiple"
    >
      <option
        disabled="disabled"
        value=""
      ><slot name="empty-option">Please select one</slot></option>
      <option
        v-for="option in options"
        :key="option"
        :value="option"
      >{{ option }}</option>
    </select>
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