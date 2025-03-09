<script setup lang="ts">
import type { Shoe } from "../scripts/types";
const props = defineProps<{
  shoeDetail: Shoe;
}>();
</script>

<template>
  <div class="shoe-card">
    <img
      :src="shoeDetail.image"
      :alt="shoeDetail.name"
      class="shoe-image rounded"
    />
    <h2>{{ props.shoeDetail.name }}</h2>
    <p><strong>Marque:</strong> {{ shoeDetail.brand }}</p>
    <p><strong>Prix:</strong> {{ shoeDetail.price }}$</p>
    <p><strong>Stock:</strong> {{ shoeDetail.stock }} disponible</p>
    <p class="description mx-auto w-75">{{ shoeDetail.description }}</p>
  </div>
</template>

<style scoped></style>
