<template>
  <div v-if="product.extras.moduleContent.product">
    <section>
      <div class="container flex flex-wrap items-center pt-4 pb-12 mx-auto">
        <div
          class="grid grid-cols-1 gap-4 mt-8 lg:grid-cols-2 xl:grid-cols-2 md:grid-cols-2 sm:grid-cols-2"
        >
          
          <div class="ml-8">
            <p class="text-3xl font-bold text-left">{{ product.extras.moduleContent.product.name }}</p>
           
            <p  class="pt-1 mt-4 text-2xl text-gray-900">
              {{ product.extras.moduleContent.product.price_from }}
            </p>
            <br />
            <p class="pt-1 mt-4 text-2xl text-gray-900">
              {{ stripHTML(product.extras.moduleContent.model.text) }}
            </p>
          
            <p
              v-if="product.variations"
              class="pt-1 mt-4 text-xl text-gray-900"
            >
              <span class="py-2">Variants</span>
              <select
                id="variant"
                name="variant"
                class="block w-64 px-6 py-2 bg-white border border-gray-500 rounded-lg focus:outline-none focus:shadow-outline"
                @change="changeVariation()"
              >
                <option
                  v-for="(variation, index) in product.variations.nodes"
                  :key="variation.databaseId"
                  :value="variation.databaseId"
                  :selected="index === 0"
                >
                  {{ variation.name }} ({{ variation.stockQuantity }} in stock)
                </option>
              </select>
            </p>
            <div class="pt-1 mt-2">
              <!-- Doesn't work?`-->
              <AddToCartButton
                v-if="product.variations"
                :product="selectedVariation"
                client:visible
              />
              <AddToCartButton v-else :product="product" client:visible />
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

import { filteredVariantPrice, stripHTML } from "../../utils/functions";

import AddToCartButton from "../../components/Cart/AddToCartButton.vue";

const props = defineProps(["product"]);

const selectedVariation = ref(18);

onMounted(() => {
  if (props.product.variations) {
    const firstVariant = props.product.variations.nodes[0].databaseId;
    selectedVariation.value = firstVariant;
  }
});

const changeVariation = (event) => {
  selectedVariation.value = event.target.value;
};
</script>
