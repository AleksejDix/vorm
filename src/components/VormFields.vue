<template>
  <component
    :is="tag"
  >
    <template
      v-for="field in schema"
    >
      <component
        :key="field.model"
        :is="field.component"
        :model-value="getValue(field)"
        @update:modelValue="update(field.model, $event)"
        v-bind="getAttributes(field)"
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
      type: Array,
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
      // eslint-disable-next-line no-unused-vars
      const {component, attrs} = field
      return attrs
    }
  }
}
</script>