<template>
    <div class="row" v-for="rowIndex in rowCount(visibleProducts)" :key="rowIndex">
        <ProductsDetail 
            v-for="product in productsForRow(rowIndex)"
            :key="product.prod_id"
            :status="product.prod_status"
            :name="product.prod_name"
            :new_price="product.prod_price"
            :old_price="product.prod_oldprice"
        />
    </div>
</template>

<script>
import ProductsDetail from "./ProductsDetail.vue";
import { reactive, onMounted } from "vue";

export default {
    props: { selectedOptions: Array },
    components: { ProductsDetail },
    setup(props) {
        let state = reactive({productsList:[]});
        const itemsPerRow = 4;
        const ignoredKeys = ["response_code"]

        function rowCount() {
            return Math.ceil(visibleProducts().length / itemsPerRow);
        }

        function productsForRow(index) {
            return visibleProducts().slice((index - 1) * itemsPerRow, index * itemsPerRow);
        }

        function visibleProducts() {
            if (props.selectedOptions.length > 0) {
                let products = [];
                state.productsList.forEach((product) => {
                    if (props.selectedOptions.some(status => product.prod_status.split(",").includes(status))) {
                        products.push(product)
                    }
                })
                return products;
            } else {
                return state.productsList
            }
        }

        onMounted(() => {
            fetch('http://localhost:3000/products.json')
                .then(res => res.json())
                .then(data => {
                    let products = [];
                    Object.keys(data).forEach((key) => {
                        if (!ignoredKeys.includes(key)) {
                            products.push(data[key])
                        }
                    })
                    state.productsList = products;
                })
                .catch(err => console.log(err.message))
        })

        return { state, itemsPerRow, rowCount, productsForRow, visibleProducts };
    },          
};
</script>