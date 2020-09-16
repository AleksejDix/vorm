<template>
  <div>
    <div>{{ $attrs.label }}</div>
    <ul
      v-for="(option, index) in model"
      :key="index"
    >
      <li>
        {{ option }}<button
          type="button"
          @click="remove(option)"
        >
          delete
        </button>
      </li>
    </ul>

    <input
      type="text"
      v-model="query"
      @keydown.enter="create"
    ><button
      type="button"
      @click="create"
    >
      add
    </button>
  </div>
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
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      query: ''
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
  },
  methods: {
    create() {
      if (this.model.includes(this.query)) return
      this.model.push(this.query)
      this.query = ''
    },
    remove(option) {
      this.model = this.model.filter(s => s !== option)
    }
  },
}
</script>
