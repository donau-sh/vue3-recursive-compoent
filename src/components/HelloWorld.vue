<template>
  <h1>Hello recuisive components</h1>
  <div id="container">
    <recursive-component 
      :characters="characters"
      :selectedItem="selected"
      :level="0"
      @selected="select"
    />
  </div>
</template>

<script setup>
import RecursiveComponent from './RecursiveComponent.vue';
import {ref} from 'vue';

const selected = ref([]);

const select = (character, level) => {
  selected.value[level] = character;
  selected.value.splice(level +1);
};

const characters = [
  {name: 'Gandalf'},
  {
    name: 'Thranduil',
    children: [
      {name: 'Legolas'}
    ]
  },
  {
    name: 'Groin son of Farin',
    children: [
      {
        name: 'Gloin son of Groin',
        children: [
          {name: 'Gimli son fo Gloin'}
        ]
      }
    ]
  }
]

// export default {
//   name: 'HelloWorld',
//   components: {
//     RecursiveComponent,
//   }
// }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

#container {
  border: 2px solid #41b883;
  display: flex;
  margin: 0 auto;
  max-width: 800px;
}
</style>
