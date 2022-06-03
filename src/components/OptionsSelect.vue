<template>
    <vue-select 
        v-model="selectedOptions" 
        :options="options" 
        multiple 
        :min="0" 
        :max="options.length" 
        close-on-select        
    />
    <br>
    <ProductsContainer :selectedOptions= "selectedOptions"/>
</template>

<script>
import ProductsContainer from "./ProductsContainer.vue"
import VueSelect from "vue-next-select";
import "vue-next-select/dist/index.min.css";
import {ref} from "vue";

export default {
    components: { VueSelect, ProductsContainer },
    setup() {
        let selectedOptions = ref([]);
        const options = ref(["recommended", "saleout", "bestseller", "promotion", "new"])
        return { options, selectedOptions }
    },
        
}
</script>