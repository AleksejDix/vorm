<template>
  <component
    :is="tag"
  >
    <template
      v-for="(v, k) in schema"
    >
      <component
        :key="k"
        :is="schema[k].component"
        :model-value="getValue(schema[k])"
        @update:modelValue="update(k, $event)"
        v-bind="getAttributes(schema[k])"
      />
    </template>
    <slot
      name="actions"
      :fields="modelValue"
    />
  </component>
</template>

<script>
export default {
  name: 'VormFields',
  model: {
    prop: 'modelValue',
    event: 'update:modelValue'
  },
  props: {
    modelValue: {
      type: Object,
      default: () => ({})
    },
    schema: {
      type: Object,
      default: () => ({})
    },
    tag: {
      type: String,
      default: 'form',
      validator: (value) => ['form', 'div'].indexOf(value) !== -1
    }
  },
  computed: {
    isRoot() {
      return this.tag === 'form'
    }
  },
  methods: {
    update(field, value){
      const form = {
        ...this.modelValue,
        [field]: value
      }
      this.$emit('update:modelValue', form)
    },
    getValue (field) {
      if (field.schema && !this.modelValue[field.model]) {
        return {}
      }

      return this.modelValue[field.model]
    },
    getAttributes (field) {
      console.log(field)
      // eslint-disable-next-line no-unused-vars
      const {component, attrs} = field
      return attrs
    }
  }
}
</script>