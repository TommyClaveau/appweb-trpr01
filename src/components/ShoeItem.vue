<script setup lang="ts">
import type { Shoe } from "../scripts/types";
import placeholderImg from "../assets/imagePlaceHolder.jpg";
import { computed } from "vue";
const props = defineProps<{
  shoe: Shoe;
  startEditShoe: (shoeId: number) => void;
  duplicateShoe: (shoeId: number) => void;
  showConfirmation: (shoeId: number) => void;
  showDetail: (shoeId: number) => void;
}>();
const stockColor = computed(() => {
  if (props.shoe.stock <= 3) return "text-danger";
  if (props.shoe.stock <= 10) return "text-warning";
  return "text-success";
});
</script>

<template>
  <tr>
    <td>
      <img
        :src="shoe.image || placeholderImg"
        :alt="shoe.name"
        class="shoe-image rounded"
      />
    </td>
    <td>{{ shoe.name }}</td>
    <td>{{ shoe.brand }}</td>
    <td :class="stockColor">{{ shoe.stock }}</td>
    <td>
      <button
        class="border border-info mx-1"
        title="Details"
        @click="showDetail(shoe.id)"
      >
        🔍
      </button>
      <button
        class="border border-light mx-1"
        @click="duplicateShoe(shoe.id)"
        title="Dupliquer"
      >
        📄
      </button>
      <button
        class="border border-warning mx-1"
        @click="startEditShoe(shoe.id)"
        title="Modifier"
      >
        ✏️
      </button>
      <button
        class="border border-danger mx-1"
        @click="showConfirmation(shoe.id)"
        title="Supprimer"
      >
        🗑️
      </button>
    </td>
  </tr>
</template>

<style scoped>
.shoe-image {
  width: 80px;
  height: 80px;
}
</style>
