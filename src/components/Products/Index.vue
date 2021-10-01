<template>
    <div class="overflow-x-auto">
        <table class="rounded-t-lg m-5 w-5/6 mx-auto bg-gray-200 text-gray-800">
            <thead>
                <tr slot="table-title" class="bg-gray-900 border-gray-200">
                    <th class="px-16 py-2">
                        <span class="text-gray-300">ID</span>
                    </th>
                    <th class="px-16 py-2">
                        <span class="text-gray-300">Nome</span>
                    </th>
                    <th class="px-16 py-2">
                        <span class="text-gray-300">Preço</span>
                    </th>
                    <th class="px-16 py-2">
                        <span class="text-gray-300">Peso</span>
                    </th>
                    <th class="px-16 py-2">
                        <span class="text-gray-300">Estoque</span>
                    </th>
                    <th class="px-16 py-2">
                        <span class="text-gray-300">Remover</span>
                    </th>
                </tr>
            </thead>
            <tbody class="bg-gray-200">
                <tr
                    class="bg-white border-4 border-gray-200"
                    v-for="product in products"
                    :key="product.id"
                    slot="table-content"
                >
                    <td class="px-16 py-2 text-center">{{ product.id }}</td>
                    <td class="px-16 py-2 text-center">{{ product.name }}</td>
                    <td class="px-16 py-2 text-center">{{ product.formate_price }}</td>
                    <td class="px-16 py-2 text-center">{{ product.formate_weight }}</td>
                    <td class="px-16 py-2 text-center">{{ product.stock }}</td>
                    <td class="px-16 py-2 text-center">
                        <button
                        @click="destroy(product.id)"
                        class="bg-red-500 text-white px-4 py-2 border rounded-md hover:bg-white hover:border-red-500 hover:text-black "
                    >
                            Remover
                        </button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
  name: "ProductsIndex",
  data() {
    return {
      products: []
    };
  },

  async created() {
    await this.getProducts();
  },

  methods: {
    async getProducts() {
      const { data: response } = await this.$axios.get("products");

      this.products = response.data;
    },

    async destroy(id) {
      const { data: response } = await this.$axios.delete(`products/${id}`);
      this.products = response.data;

      this.getProducts();
    },
  },
};
</script>
