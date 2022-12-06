<template>
    <ul class="character-list">
  
      <template v-for="character of characters" :key="character.name">
  
        <li :class="{ selected: isSelected(character) }" 
            @click="select(character, level)"
        >
          <div class="name">{{ character.name }}</div>
  
          <template v-if="isSelected(character)">
            <teleport to="#container">
              <recursive-component
                v-if="character.children"
                :characters="character.children"
                :selectedItem="selected"
                :level="level + 1"
                @selected="select"
              />
            </teleport>
          </template>
        </li>
  
      </template>
  
    </ul>
  
  </template>

<script>
// const emit = defineEmits(['selected']);

// const select = (route, level) => {
//     emit('selected', route, level);
// }

// const isSelected = (character) => {
//     if (!props.selected || !props.selected.length || !props.selected.some(char => char.name === character.name)) {
//         return false;
//     }
//     return props.selected[props.level]?.name === character.name;
// };

import {ref} from 'vue';

    export default {
        name: 'RecursiveComponent',

        props: {
            characters: {
                type: Array,
                required: true
            },
            selectedItem: {
                type: Array,
                required: false,
                default: ref([]),
            },
            level: {
                type: Number,
                required: false,
                default: 0,
            }
        },

        emits: ['selected'],

        computed: {
            
        },

        methods: {
            select (route, level) {
                this.$emit('selected', route, level);
            },

            isSelected (character){
                if (!this.selectedItem || !this.selectedItem.length || !this.selectedItem.some(char => char.name === character.name)) {
                    return false;
                }
                return this.selectedItem[this.level]?.name === character.name;
            }
        }
    }
   

    
</script>

<style scoped>
.character-list {
    border-right: 1px solid #41b883;
    min-height: 25vh;
    width: 200px;
    margin: 0;
    padding: 0;
}
.character-list li {
    padding: 0.5em 1em;
}
.character-list li:hover {
    cursor: pointer;
}
.character-list li:not(.selected):hover {
    background-color: rgba(0, 0, 0, 0.05);
}
.character-list li.selected {
    background-color: rgba(0, 0, 0, 0.1);
}
</style>