<template>
  <div id="app">
    <pre>{{ model }}</pre>
    <pre>{{ schema }}</pre>
    <VormFields
      v-model="model"
      :schema="schema"
    >
      <template #actions="{fields}">
        <div>
          <button
            type="submit"
            @click.prevent="handleSubmit(fields)"
          >
            submit
          </button>
        </div>
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
Vue.component('VormSelect', () => import('@/components/fields/VormSelect'))
Vue.component('VormChoise', () => import('@/components/fields/VormChoise'))


export default {
  components: {
    VormFields,
  },
  data() {
    return {
      model: {
        car: 'Audi',
        fruits: ['apple', 'peach'],
        person: 'Aleksej',
        people: ['Aleksej'],
      }
    }
  },
  computed: {
    schema() {
      return [
        {
          component: 'VormSelect',
          model: 'car',
          attrs: {
            label: 'car',
            options: [
              'Audi',
              'Saab',
              'Volvo',
            ]
          }
        },
        {
          component: 'VormSelect',
          model: 'cars',
          attrs: {
            label: 'car',
            multiple: true,
            options: [
              'Audi',
              'Saab',
              'Volvo',
            ]
          }
        },
        {
          component: 'VormChoise',
          model: 'people',
          attrs: {
            label: 'people',
            multiple: true,
            options: [
              'Aleksej',
              'Lidia',
            ]
          }
        },
        {
          component: 'VormChoise',
          model: 'person',
          attrs: {
            label: 'person',
            options: [
              'Aleksej',
              'Lidia',
            ]
          }
        },
        {
          component: 'VormString',
          model: 'name',
          attrs: {
            label: 'name',
            required: true,
            pattern: '[a-zA-Z0-9]+',
            placeholder: 'try it out'
          }
        },
        {
          component: 'VormRepeater',
          model: 'fruits',
          attrs: {
            label: 'fruits'
          }
        },
        {
          component: 'VormBoolean',
          model: 'accept',
          attrs: {
            label: 'accept'
          }
        },
        {
          component: 'VormText',
          model: 'comment',
          attrs: {
            label: 'comment'
          }
        }
      ]
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

input[type="text"],
textArea,
select {
  width: 100%
}
</style>
