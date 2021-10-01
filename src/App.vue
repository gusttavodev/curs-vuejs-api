<template>
    <div id="app">
        <TheHeader />

        <div class="px-3 py-10 md:px-10">
            <ProductsIndex/>
            <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
        </div>
    </div>
</template>

<script>
    import TheHeader from "./components/Partials/TheHeader.vue"
    import ProductsIndex from './components/Products/Index.vue'
    // import HelloWorld from './components/HelloWorld.vue'

    export default {
        name: 'App',

        components: {
          TheHeader,
          ProductsIndex
        //   HelloWorld
        },

        data() {
            return {
            };
        },

        methods: {},
    };
</script>
