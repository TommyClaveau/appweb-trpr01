<script setup lang="ts">
import { ref } from "vue";
const props = defineProps<{
  shoeName: string;
  shoeBrand: string;
  shoePrice: number;
  shoeStock: number;
  shoeImage: string;
  shoeDescription: string;
  addShoe: () => void;
}>();
const emit = defineEmits([
  "update:shoeName",
  "update:shoeBrand",
  "update:shoePrice",
  "update:shoeStock",
  "update:shoeImage",
  "update:shoeDescription",
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
  if (!props.shoeName.trim()) {
    errors.value.shoeName = true;
    isValid = false;
  }
  if (!props.shoeBrand.trim()) {
    errors.value.shoeBrand = true;
    isValid = false;
  }
  if (props.shoePrice < 0) {
    errors.value.shoePrice = true;
    isValid = false;
  }
  if (props.shoeStock < 0) {
    errors.value.shoeStock = true;
    isValid = false;
  }
  if (isValid) {
    resetErrors();
    props.addShoe();
  }
};
</script>

<!--TODO readme utilisation de chatpt pour la couleur des labels-->
<template>
  <div class="container mt-4">
    <h3 class="mb-3">Ajouter une paire</h3>
    <div class="card p-4 shadow-sm">
      <div class="mb-3">
        <label for="shoeName" class="form-label">Nom de la paire * </label>
        <input
          id="shoeName"
          type="text"
          class="form-control"
          :value="shoeName"
          @input="
            emit('update:shoeName', ($event.target as HTMLInputElement).value)
          "
          placeholder="Entrez le nom de la paire"
        />
        <p v-if="errors.shoeName" class="text-danger">
          Veuillez entrer un nom pour la paire
        </p>
      </div>

      <div class="mb-3">
        <label for="shoeBrand" class="form-label">Nom de la marque *</label>
        <input
          id="shoeBrand"
          type="text"
          class="form-control"
          :value="shoeBrand"
          @input="
            emit('update:shoeBrand', ($event.target as HTMLInputElement).value)
          "
          placeholder="Entrez la marque"
        />
        <p v-if="errors.shoeBrand" class="text-danger">
          Veuillez entrer une marque pour la paire
        </p>
      </div>

      <div class="mb-3">
        <label for="shoePrice" class="form-label">Prix de la paire *</label>
        <input
          id="shoePrice"
          type="number"
          class="form-control"
          :value="shoePrice"
          @input="
            emit(
              'update:shoePrice',
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
        <label for="shoeStock" class="form-label">Nombre en stock *</label>
        <input
          id="shoeStock"
          type="number"
          class="form-control"
          :value="shoeStock"
          @input="
            emit(
              'update:shoeStock',
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
        <label for="shoeDescription" class="form-label"
          >Description de la paire</label
        >
        <textarea
          id="shoeDescription"
          type="text"
          class="form-control"
          rows="3"
          :value="shoeDescription"
          @input="
            emit(
              'update:shoeDescription',
              ($event.target as HTMLInputElement).value
            )
          "
          placeholder="Entrez une description"
        />
      </div>
      <div class="mb-3">
        <label for="shoeImage" class="form-label">Image de la paire</label>
        <input
          id="shoeImage"
          type="text"
          class="form-control"
          :value="shoeImage"
          @input="
            emit('update:shoeImage', ($event.target as HTMLInputElement).value)
          "
          placeholder="Image possible"
        />
      </div>
      <button class="btn btn-primary w-100" @click="validateFields">
        Ajouter
      </button>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 500px;
}
.text-danger {
  color: red;
}
.invalid-feedback {
  color: red;
}
</style>
