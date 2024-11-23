<script setup lang="ts">
import { ref } from 'vue'
import { ComboboxAnchor, ComboboxContent, ComboboxEmpty, ComboboxGroup, ComboboxInput, ComboboxItem, ComboboxItemIndicator, ComboboxLabel, ComboboxPortal, ComboboxRoot, ComboboxSeparator, ComboboxTrigger, ComboboxViewport, PopoverAnchor, PopoverArrow, PopoverClose, PopoverContent, PopoverPortal, PopoverRoot, PopoverTrigger, ScrollAreaCorner, ScrollAreaRoot, ScrollAreaScrollbar, ScrollAreaThumb, ScrollAreaViewport } from 'reka-ui'


const otherPeople = [
  { _id: 6, display: 'Jean mich' },
  { _id: 7, display: 'Jeanette' },
  { _id: 8, display: 'Jean' },
  { _id: 9, display: 'Albert roturier' },
] // the query here is minimal so this can be very fast
const reactiveList = ref(JSON.parse(JSON.stringify(otherPeople)))

const selectedPeople = ref([{
  ...otherPeople[0],
  someOtherFieldUsedInjoin: 'dadad' // beacause the join from bdd have this field on inital page load
}])


function filterFunction(list: typeof people[number], searchTerm: string) {
  return list.filter((person) => {
    return person.display.toLowerCase().includes(searchTerm.toLowerCase())
  })
}
</script>

<template>

  <pre>{{ reactiveList }}</pre>
  {{ selectedPeople }}
  <ComboboxRoot v-model="selectedPeople" :display-value="(v) => v.display" style="position: relative;" multiple :filter-function="filterFunction" ignore-filter>
    <ComboboxAnchor>

      <ComboboxInput />
    </ComboboxAnchor>
    <ComboboxPortal>
      <ComboboxContent style="width: var(--reka-popper-anchor-width); width: 100%;" position="popper">
        <ComboboxViewport class="">
          <ComboboxItem class="highlighted" v-for="person in reactiveList" :key="person._id" :value="person"
            :disabled="person.unavailable" style="padding-left: 15px;">

            <ComboboxItemIndicator style="position: absolute; left: 0px;">
              ✔
            </ComboboxItemIndicator>
            {{ person.display }}
          </ComboboxItem>
        </ComboboxViewport>

      </ComboboxContent>
    </ComboboxPortal>
  </ComboboxRoot>
</template>

<style>
.highlighted {
  cursor: pointer;
}

.highlighted[data-highlighted] {
  background-color: blue;
  /* Remplacez par votre couleur */
  color: white;
  /* Remplacez par votre couleur */
}
</style>