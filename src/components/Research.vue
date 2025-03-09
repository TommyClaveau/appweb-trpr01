<script setup lang="ts">
const props = defineProps<{
  researchShoeName: string;
  researchShoe: () => void;
}>();
const emit = defineEmits(["update:researchShoeName"]);
</script>

<template>
  <div>
    <input
      class="form-control"
      type="text"
      :value="props.researchShoeName"
      @input="
        emit(
          'update:researchShoeName',
          ($event.target as HTMLInputElement).value
        );
        researchShoe();
      "
      placeholder="Rechercher"
    />
  </div>
</template>

<style scoped></style>
