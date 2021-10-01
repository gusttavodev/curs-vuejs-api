<template>
    <div id="app">
        <TheHeader />

        <div class="px-3 py-10 md:px-10">
            <ProductForm
                @onCreate="onCreateProduct"
            />
            <ProductsIndex ref="productsIndex"/>
            <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
        </div>
    </div>
</template>

<script>
    import TheHeader from "./components/Partials/TheHeader.vue"
    import ProductsIndex from './components/Products/Index.vue'
    import ProductForm from './components/Products/Form.vue'
    // import HelloWorld from './components/HelloWorld.vue'

    export default {
        name: 'App',

        components: {
          TheHeader,
          ProductsIndex,
          ProductForm
        //   HelloWorld
        },

        data() {
            return {
            };
        },

        methods: {
            async onCreateProduct(){
                await this.$refs.productsIndex.getProducts()
            }
        },
    };
</script>
