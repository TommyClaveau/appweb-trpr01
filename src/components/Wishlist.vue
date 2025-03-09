<script setup lang="ts">
import { ref } from "vue";
import { computed } from "vue";
import type { Shoe } from "../scripts/types";
import ShoeItem from "./ShoeItem.vue";
import AddShoe from "./AddShoe.vue";
import EditShoe from "./EditShoe.vue";
import Research from "./Research.vue";
import Detail from "./Detail.vue";
import { watch } from "vue";

const shoes = ref<Shoe[]>([
  {
    id: 1,
    name: "airforce 1",
    brand: "nike",
    price: 99.99,
    stock: 20,
    description:
      "Ces souliers sont un classic, cette paire peut être assortie avec tes meilleurs styles!!!!!",
    image:
      "data:image/jpeg;base64,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",
  },
  {
    id: 2,
    name: "Air Jordan",
    brand: "Nike",
    price: 129.99,
    stock: 5,
    description:
      "Pour les amateurs de basket ou de mode, les jordans sont un incontournable",
    image:
      "data:image/jpeg;base64,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",
  },
  {
    id: 3,
    name: "Flash Mcqueen",
    brand: "Crocs",
    price: 999.99,
    stock: 1,
    description: "La beaute et la finesse absolue, à acheter!",
    image:
      "https://encrypted-tbn1.gstatic.com/shopping?q=tbn:ANd9GcS9BO7g-lQ6mjar6qcng4ORUJjYdy7y4bdo53kWuZ4CpPDyob50Cp81XZyz0yZPdYMAVk-yC3u2cwCWbrY2YWqxgeJdSSvlN162OoCXwII",
  },
]);
const researchedShoes = ref<Shoe[]>([]);

const displayedShoes = computed(() => {
  if (researchShoeName.value) {
    return researchedShoes.value;
  }
  return shoes.value;
});

const shoeName = ref<string>("");
const shoeBrand = ref<string>("");
const shoePrice = ref<number>(0);
const shoeStock = ref<number>(0);
const shoeDescription = ref<string>("");
const shoeImage = ref<string>("");

const selectedShoeId = ref<number>(0);

const editShoeName = ref<string>("");
const editShoeBrand = ref<string>("");
const editShoePrice = ref<number>(0);
const editShoeStock = ref<number>(0);
const editShoeDescription = ref<string>("");
const editShoeImage = ref<string>("");

const researchShoeName = ref<string>("");

const selectedAction = ref<"add" | "edit" | "detail">("add");

const isConfirmationShown = ref(false);
const shoeToRemove = ref<number | null>(null);

const shoeDetail = ref<Shoe>({
  id: 0,
  name: "",
  brand: "",
  price: 0,
  stock: 0,
  description: "",
  image: "",
});

const resetAddFields = () => {
  shoeName.value = "";
  shoeBrand.value = "";
  shoePrice.value = 0;
  shoeStock.value = 0;
  shoeDescription.value = "";
  shoeImage.value = "";
};
const addShoe = () => {
  shoes.value.push({
    id: Date.now(),
    name: shoeName.value,
    brand: shoeBrand.value,
    price: shoePrice.value,
    stock: shoeStock.value,
    description: shoeDescription.value,
    image: shoeImage.value,
  });
  resetAddFields();
};
const editShoe = () => {
  if (!editShoeName.value.trim() || !editShoeBrand.value.trim()) return;
  const shoe = shoes.value.find((shoe) => shoe.id === selectedShoeId.value);
  if (shoe) {
    shoe.name = editShoeName.value;
    shoe.brand = editShoeBrand.value;
    shoe.price = editShoePrice.value;
    shoe.stock = editShoeStock.value;
    shoe.description = editShoeDescription.value;
    shoe.image = editShoeImage.value;
  }
  editShoeName.value = "";
  editShoeBrand.value = "";
  editShoePrice.value = 0;
  editShoeStock.value = 0;
  editShoeImage.value = "";
  editShoeDescription.value = "";
  selectedAction.value = "add";
};
const startEditShoe = (shoeId: number) => {
  selectedShoeId.value = shoeId;
  const shoe = shoes.value.find((shoe) => shoe.id === shoeId);
  if (shoe) {
    editShoeName.value = shoe.name;
    editShoeBrand.value = shoe.brand;
    editShoePrice.value = shoe.price;
    editShoeStock.value = shoe.stock;
    editShoeDescription.value = shoe.description;
    editShoeImage.value = shoe.image;
  }
  selectedAction.value = "edit";
};
const showDetail = (shoeId: number) => {
  const shoe = shoes.value.find((shoe) => shoe.id === shoeId);
  if (shoe) {
    shoeDetail.value = shoe;
  }
  selectedAction.value = "detail";
};
const duplicateShoe = (shoeId: number) => {
  selectedAction.value = "add";
  const shoe = shoes.value.find((shoe) => shoe.id === shoeId);
  if (shoe) {
    shoeName.value = shoe.name;
    shoeBrand.value = shoe.brand;
    shoePrice.value = shoe.price;
    shoeStock.value = shoe.stock;
    shoeDescription.value = shoe.description;
    shoeImage.value = shoe.image;
  }
};
const showConfirmation = (shoeId: number) => {
  shoeToRemove.value = shoeId;
  isConfirmationShown.value = true;
};
const removeShoe = () => {
  shoes.value = shoes.value.filter((shoe) => shoe.id !== shoeToRemove.value);
  shoeToRemove.value = null;
  isConfirmationShown.value = false;
  selectedAction.value = "add";
};
const researchShoe = () => {
  if (!researchShoeName.value.trim()) {
    researchedShoes.value = [];
    return;
  }
  researchedShoes.value = shoes.value.filter((shoe) =>
    shoe.name.toLowerCase().includes(researchShoeName.value.toLowerCase())
  );
};

//SRC : https://stackoverflow.com/questions/74423711/save-csv-from-an-array-of-objects-in-vuejs-3

const arrayToCsv = (data: any[]): string => {
  const array = [Object.keys(data[0])].concat(data);

  return array
    .map((it) => {
      return Object.values(it).toString();
    })
    .join("\n");
};
const downloadBlob = (
  content: string,
  filename: string,
  contentType: string
) => {
  var blob = new Blob([content], { type: contentType });
  var url = URL.createObjectURL(blob);

  // Create a link to download it
  var pom = document.createElement("a");
  pom.href = url;
  pom.setAttribute("download", filename);
  pom.click();
};
const exportToCsv = () => {
  const csv = arrayToCsv(shoes.value);
  downloadBlob(csv, "shoes_list.csv", "text/csv;charset=utf-8;");
};

const notifyLowStock = (shoe: Shoe) => {
  if (shoe.stock === 0) {
    alert("Le produit " + shoe.name + " est hors de stock.");
  }
};
watch(
  shoes,
  (newShoes) => {
    newShoes.forEach((shoe) => {
      if (shoe.stock === 0) {
        notifyLowStock(shoe);
      }
    });
  },
  { deep: true }
);
</script>

<template>
  <div v-if="isConfirmationShown">
    <div class="bg-custom-dark m-auto my-3 w-25 border-warning">
      <p>Voulez-vous vraiment supprimer ce soulier ?</p>
      <button class="border border-danger mx-1" @click="removeShoe">Oui</button>
      <button
        class="border border-green mx-1"
        @click="isConfirmationShown = false"
      >
        Annuler
      </button>
    </div>
  </div>
  <div
    class="d-flex justify-content-center align-items-start gap-5 w-100 mt-5 mb-5 rounded"
  >
    <div class="wishlist">
      <div class="d-flex align-items-center mb-3">
        <Research
          v-model:researchShoeName="researchShoeName"
          :researchShoe="researchShoe"
        />
        <button class="border border-success mx-2" @click="exportToCsv">
          Export
        </button>
        <button
          @click="
            selectedAction = 'add';
            resetAddFields();
          "
          class="border border-primary"
        >
          Ajouter une paire
        </button>
      </div>
      <div class="bg-custom-dark px-3 pb-3 rounded">
        <h1>Ma liste</h1>
        <table
          class="list-shoe table table-striped mb-0"
          v-if="displayedShoes.length"
        >
          <thead class="thead">
            <tr>
              <th>Image</th>
              <th>Nom</th>
              <th>Marque</th>
              <th>Stock</th>
              <th>Actions</th>
            </tr>
          </thead>
          <tbody class="tbody">
            <ShoeItem
              v-for="shoe in displayedShoes"
              :key="shoe.id"
              :shoe="shoe"
              :startEditShoe="startEditShoe"
              :duplicateShoe="duplicateShoe"
              :showDetail="showDetail"
              :showConfirmation="showConfirmation"
            />
          </tbody>
        </table>
        <p class="text-center text-muted" v-else>
          Aucun soulier pour le moment
        </p>
      </div>
    </div>
    <div class="pannel bg-custom-dark rounded pb-5">
      <div class="d-flex justify-content-between mb-3"></div>
      <AddShoe
        v-if="selectedAction === 'add'"
        v-model:shoeName="shoeName"
        v-model:shoeBrand="shoeBrand"
        v-model:shoePrice="shoePrice"
        v-model:shoeStock="shoeStock"
        v-model:shoeImage="shoeImage"
        v-model:shoeDescription="shoeDescription"
        :addShoe="addShoe"
      />
      <EditShoe
        v-if="selectedAction === 'edit'"
        v-model:editShoeName="editShoeName"
        v-model:editShoeBrand="editShoeBrand"
        v-model:editShoePrice="editShoePrice"
        v-model:editShoeStock="editShoeStock"
        v-model:editShoeImage="editShoeImage"
        v-model:editShoeDescription="editShoeDescription"
        :editShoe="editShoe"
      />
      <Detail
        v-if="selectedAction === 'detail'"
        v-model:shoeDetail="shoeDetail"
      />
    </div>
  </div>
</template>

<style scoped>
.wishlist {
  width: 60%;
}
.pannel {
  width: 30%;
}
</style>
