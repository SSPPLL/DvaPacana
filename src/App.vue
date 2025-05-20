<script setup lang="ts">
import Cloth                     from "./components/Cloth.vue";
import { computed, ref }         from "vue";
import Clothes                   from "./components/Clothes.vue";
import type { TCloth }           from "./types.ts";
import { leftItems, rightItems } from "./data.ts";

const nothingToShowText = 'Ничего не выбрано';
const leftSelected      = ref<Set<TCloth>>(new Set<TCloth>());
const rightSelected     = ref<TCloth | null>(null);
const leftItemsList     = computed(() => leftItems.filter((item) => !leftSelected.value.has(item)));
const rightItemsList    = computed(() => rightItems.filter((item) => item.id !== rightSelected.value?.id));

function onSelect(item: TCloth, side: 'left' | 'right') {
  if (side === 'right' && !rightSelected.value) {
    rightSelected.value = item
  }

  if (side === 'left' && leftSelected.value.size < 6) {
    leftSelected.value.add(item)
  }
}
</script>

<template>
  <div class="container mx-auto p-2 flex flex-col gap-10">
    <div class="flex justify-between">
      <div
        :class="[
          'flex flex-wrap w-70 h-70',
          'border-1 border-solid border-black p-2 rounded-md gap-2',
          {
            'content-start items-start justify-start': leftSelected.size,
            'justify-center items-center text-center text-2xl': !leftSelected.size
          }
        ]">
        {{ !leftSelected.size ? nothingToShowText : '' }}
        <Cloth
          v-for="item in leftSelected"
          :name="item.name"
          :key="item.id"
          @click="leftSelected.delete(item)"/>
      </div>
      <button
        :class="[
          'flex justify-center items-center text-center text-2xl w-70 h-70 border-1 border-solid border-black',
          'p-2 rounded-md select-none cursor-pointer appearance-none outline-none',
        ]"
        @click="rightSelected = null">
        {{ rightSelected ? rightSelected.name : nothingToShowText }}
      </button>
    </div>
    <div class="grid grid-cols-2 gap-10">
      <Clothes>
        <Cloth
          v-for="item in leftItemsList"
          :name="item.name"
          :key="item.id"
          @click="onSelect(item, 'left')"/>
      </Clothes>
      <Clothes>
        <Cloth
          v-for="item in rightItemsList"
          :name="item.name"
          :key="item.id"
          @click="onSelect(item, 'right')"/>
      </Clothes>
    </div>
  </div>
</template>

<style>
</style>
