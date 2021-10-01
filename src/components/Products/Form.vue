<template>
<div>
  <h3 class="text-xl text-center p-5 text-gray-500 ml-2">
    Cadastrar Produto
  </h3>
  <div
    v-if="response.messages.length > 0"
    :class="`rounded-sm bg-${response.color}-100 p-4 mb-4`"
  >
    <h3 
      v-for="(message, index) in response.messages"
      :key="index"
      :class="`text-sm leading-5 font-medium text-${response.color}-800`"
    >
      {{ message[0] }}
    </h3>
  </div>

  <form class="grid grid-cols-12 gap-2" @submit.stop.prevent="store()">
    <div class="col-span-6">
      <label class="text-white relative inline-flex items-center text-sm leading-5 font-medium">
              Nome
      </label>
      <input
          v-model="form.name"
          type="text"
          placeholder="Digite o Nome"
          class="bg-gray-900 placeholder-gray-700 text-gray-500 font-light border border-gray-900 focus:outline-none focus:border-blue-800 rounded-sm py-3 px-4 block w-full appearance-none leading-normal"
      />
    </div>

    <div class="col-span-6">
      <label class="text-white relative inline-flex items-center text-sm leading-5 font-medium">
              Preço
      </label>
      <input
        v-model="form.price"
        type="number"
        step="0.01"
        placeholder="Digite o Preço"
        class="col-span-6 bg-gray-900 placeholder-gray-700 text-gray-500 font-light border border-gray-900 focus:outline-none focus:border-blue-800 rounded-sm py-3 px-4 block w-full appearance-none leading-normal"
      />
    </div>

    <div class="col-span-6">
      <label class="text-white relative inline-flex items-center text-sm leading-5 font-medium">
        Quantidade em estoque
      </label>
      <input
        v-model="form.stock"
        type="number"
        placeholder="Quantidade em estoque"
        class="col-span-6 bg-gray-900 placeholder-gray-700 text-gray-500 font-light border border-gray-900 focus:outline-none focus:border-blue-800 rounded-sm py-3 px-4 block w-full appearance-none leading-normal"
      />
    </div>

    <div class="col-span-6">
      <label class="text-white relative inline-flex items-center text-sm leading-5 font-medium">
              Peso do produto
      </label>
      <input
          v-model="form.weight"
          type="number"
          step="0.01"
          placeholder="Peso do Produto"
          class="col-span-6 bg-gray-900 placeholder-gray-700 text-gray-500 font-light border border-gray-900 focus:outline-none focus:border-blue-800 rounded-sm py-3 px-4 block w-full appearance-none leading-normal"
      />
    </div>
    <button
        type="submit"
        class="col-span-12 justify-center bg-blue-800 text-blue-200 font-medium text-sm focus:outline-none rounded-sm py-3 px-4 block w-full appearance-none leading-normal"
    >
        Cadastrar
    </button>
  </form>

</div>
</template>

<script>
export default {
  name: "ProductForm",
  data() {
    return {
      form: {
        name: "",
        price: 0,
        stock: 0,
        weight: 0,
      },

      response: {
        color: "",
        messages: [],
      },
    };
  },

  methods: {
    async store() {
      try {
        this.resetResponse();

         await this.$axios.post("products", this.form)
        this.response.color = "green";
        this.response.messages[0] = ["Produto cadastrado com sucesso."];

        this.resetForm();
        this.$emit('onCreate')
        setTimeout(() => { 
          this.resetResponse()
        }, 2000); // 2 seconds

      } catch (error) {
        let errorMessage = error?.response?.data?.errors;        
        this.response.color = "red";
        this.response.messages = Object.values(errorMessage)

      }     
    },

    resetResponse() {
      this.response.color = "";
      this.response.messages = [];
    },
    resetForm() {
      this.form.name = "";
      this.form.price = 0;
      this.form.stock = 0;
      this.form.weight = 0;
    },
  },
};
</script>
