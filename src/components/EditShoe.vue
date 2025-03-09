<script setup lang="ts">
import { ref } from "vue";
const props = defineProps<{
  editShoeName: string;
  editShoeBrand: string;
  editShoePrice: number;
  editShoeStock: number;
  editShoeImage: string;
  editShoeDescription: string;
  editShoe: () => void;
}>();
const emit = defineEmits([
  "update:editShoeName",
  "update:editShoeBrand",
  "update:editShoePrice",
  "update:editShoeStock",
  "update:editShoeImage",
  "update:editShoeDescription",
]);
const errors = ref({
  shoeName: false,
  shoeBrand: false,
  shoePrice: false,
  shoeStock: false,
});
const resetErrors = () => {
  errors.value.shoeName = false;
  errors.value.shoeBrand = false;
  errors.value.shoePrice = false;
  errors.value.shoeStock = false;
};
const validateFields = () => {
  let isValid = true;
  resetErrors();
  if (!props.editShoeName.trim()) {
    errors.value.shoeName = true;
    isValid = false;
  }
  if (!props.editShoeBrand.trim()) {
    errors.value.shoeBrand = true;
    isValid = false;
  }
  if (props.editShoePrice < 0) {
    errors.value.shoePrice = true;
    isValid = false;
  }
  if (props.editShoeStock < 0) {
    errors.value.shoeStock = true;
    isValid = false;
  }
  if (isValid) {
    resetErrors();
    props.editShoe();
  }
};
</script>

<template>
  <div class="container mt-4">
    <h3 class="mb-3">Modifier une paire</h3>
    <div class="card p-4 shadow-sm">
      <div class="mb-3">
        <label for="editShoeName" class="form-label">Nom de la paire *</label>
        <input
          id="editShoeName"
          type="text"
          class="form-control"
          :value="editShoeName"
          @input="
            emit(
              'update:editShoeName',
              ($event.target as HTMLInputElement).value
            )
          "
          placeholder="Entrez le nom de la paire"
        />
        <p v-if="errors.shoeName" class="text-danger">
          Veuillez entrer un nom pour la paire
        </p>
      </div>

      <div class="mb-3">
        <label for="editShoeBrand" class="form-label">Nom de la marque *</label>
        <input
          id="editShoeBrand"
          type="text"
          class="form-control"
          :value="editShoeBrand"
          @input="
            emit(
              'update:editShoeBrand',
              ($event.target as HTMLInputElement).value
            )
          "
          placeholder="Entrez la marque"
        />
        <p v-if="errors.shoeBrand" class="text-danger">
          Veuillez entrer une marque pour la paire
        </p>
      </div>

      <div class="mb-3">
        <label for="editShoePrice" class="form-label">Prix de la paire *</label>
        <input
          id="editShoePrice"
          type="number"
          class="form-control"
          :value="editShoePrice"
          @input="
            emit(
              'update:editShoePrice',
              ($event.target as HTMLInputElement).valueAsNumber || 0
            )
          "
          placeholder="Entrez le prix"
        />
        <p v-if="errors.shoePrice" class="text-danger">
          Veuillez entrer un prix valide pour la paire
        </p>
      </div>

      <div class="mb-3">
        <label for="editShoeStock" class="form-label">Nombre en stock *</label>
        <input
          id="editShoeStock"
          type="number"
          class="form-control"
          :value="editShoeStock"
          @input="
            emit(
              'update:editShoeStock',
              ($event.target as HTMLInputElement).valueAsNumber || 0
            )
          "
          placeholder="Entrez la quantité en stock"
        />
        <p v-if="errors.shoeStock" class="text-danger">
          Veuillez entrer un stock valide pour la paire
        </p>
      </div>

      <div class="mb-3">
        <label for="editShoeDescription" class="form-label"
          >Description de la paire</label
        >
        <textarea
          id="editShoeDescription"
          type="text"
          class="form-control"
          rows="3"
          :value="editShoeDescription"
          @input="
            emit(
              'update:editShoeDescription',
              ($event.target as HTMLInputElement).value
            )
          "
          placeholder="Entrez la marque"
        />
      </div>
      <div class="mb-3">
        <label for="editShoeImage" class="form-label">Image de la paire </label>
        <input
          id="editShoeImage"
          type="text"
          class="form-control"
          :value="editShoeImage"
          @input="
            emit(
              'update:editShoeImage',
              ($event.target as HTMLInputElement).value
            )
          "
          placeholder="Image possible"
        />
      </div>
      <button class="btn btn-warning w-100" @click="validateFields">
        Modifier
      </button>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 500px;
}
</style>
