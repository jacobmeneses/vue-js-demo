<script setup>
import { ref } from 'vue'


const cards = ref([{
  title: 'Card 1',
  content: 'This is card 1 content',
  description: 'Description 2 slorem ipsum dolor sit amet consectetur adipiscing elit sed do eiusmod tempor incididunt ut labore et dolore magna aliqua'
}, {
  title: 'Card 2',
  content: 'This is card 2 content',
  description: 'Description 2 lorem ipsum dolor sit amet consectetur adipiscing elit sed do eiusmod tempor incididunt ut labore et dolore magna aliqua'
}
]);

const selectedCard = ref({
  title: 'Selected Card',
  description: 'This is the detailed description of the selected card. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.'
});
const detailClass = ref('border-dashed rounded-sm border-gray-400 row-span-2 hidden');
const detailOn = ref(false);
const mainGridClass = ref('grid grid-cols-1')

function onDetailFlagChanged(){
  if (detailOn.value){
    detailClass.value = detailClass.value.replace('hidden','block');
    mainGridClass.value = mainGridClass.value.replace('grid-cols-1','grid-cols-2');
  } else {
    detailClass.value = detailClass.value.replace('block','hidden');
    mainGridClass.value = mainGridClass.value.replace('grid-cols-2','grid-cols-1');
  }
}

function test(){
  detailOn.value = !detailOn.value;
  console.log('detailOn=', detailOn.value);
  onDetailFlagChanged();
}

function detail(card){
  selectedCard.value = card;
  detailOn.value = true;
  onDetailFlagChanged();
}

</script>

<template>
  <div>
    <button @click="test" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-sm">
      Test
    </button>
  </div>

  <div :class="mainGridClass">
    <div>
      <div v-for="card in cards" @click="() => detail(card)" :key="card.title" class="m-1 p-2 border border-gray-300 rounded-sm">
        <h2 class="text-xl font-semibold mb-2">{{ card.title }}</h2>
        <p>{{ card.content }}</p>
      </div>
    </div>

    <div :class="detailClass">
      <h2 class="text-xl font-semibold mb-2">{{ selectedCard.title }}</h2>
      <p>{{ selectedCard.description }}</p>
    </div>
  </div>

</template>

<style>
@import "tailwindcss";
</style>
