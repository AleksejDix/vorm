<template>
  <div id="app">
    <pre>{{ model }}</pre>
    <pre>{{ schema }}</pre>
    <VormFields
      v-model="model"
      :schema="schema"
    >
      <template #actions="{fields}">
        <button
          type="button"
          @click="handleSubmit(fields)"
        >
          submit
        </button>
      </template>
    </VormFields>
  </div>
</template>

<script>
import Vue from 'vue'
import VormFields from '@/components/VormFields.vue'


Vue.component('VormString', () => import('@/components/fields/VormString'))
Vue.component('VormBoolean', () => import('@/components/fields/VormBoolean'))
Vue.component('VormText', () => import('@/components/fields/VormText'))
Vue.component('VormRepeater', () => import('@/components/fields/VormRepeater'))


export default {
  components: {
    VormFields,
  },
  data() {
    return {
      model: {
        fruits: ['apple', 'peach']
      }
    }
  },
  computed: {
    schema() {
      return {
        name: {
          component: 'VormString',
          model: 'name',
          attrs: {
            label: 'name',
          }
        },
        fruits: {
          component: 'VormRepeater',
          model: 'fruits',
          attrs: {
            label: 'fruits'
          }
        },
        accept: {
          component: 'VormBoolean',
          model: 'accept',
          attrs: {
            label: 'accept'
          }
        },
        comment: {
          component: 'VormText',
          model: 'comment',
          attrs: {
            label: 'comment'
          }
        }
      }
    }
  },
  methods: {
    handleSubmit(payload) {
      console.log(payload)
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
}


#app > * {
  flex: 0 0 320px;
}

input,
textArea {
  border: 1px solid #ccc;
  border-radius: 0.25rem
}
</style>
