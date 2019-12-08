<template>
  <div id="app">
    <form id="form" @submit.prevent="formSubmit" action="/localhost:3000/">
      <p>nazwa produktu:</p>
      <input v-model.lazy="productName" placeholder="nazwa produktu" />
      <p>model produktu:</p>
      <input v-model.trim="productModel" placeholder="model produktu" />
      <p>opis produktu:</p>
      <textarea v-model.trim="prodDescription" placeholder="opis"></textarea>
      <p>cena promocyjna:</p>
      <input v-model.number="promoPrice" type="number" placeholder="cena" />
      <br /><br />
      <p>dodatkowe pola:</p>
      <div class="form-group" v-for="(input, k) in inputs" :key="k">
        <input type="text" class="form-control" v-model="input.name" />
        <input type="text" class="form-control" v-model="input.value" />
        <span>
          <button @click="remove(k)" v-show="k || (!k && inputs.length > 1)">
            Remove
          </button>
          <button @click="add(k)" v-show="k == inputs.length - 1">
            Add
          </button>
        </span>
      </div>
      <br /><br />
      <button>submit</button>
      <button @click="resetForm">RESET</button>
    </form>
    <br /><br />
    <div>
      <p>nazwa produktu: {{ productName }}</p>
      <p>model produktu: {{ productModel }}</p>
      <p>opis: {{ prodDescription }}</p>
      <p>cena: {{ prodPrice }}</p>
      <p>cena promocyjna: {{ promoPrice }}</p>
      <div>custom input: {{ inputs }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      ts: this.submitted,
      productName: "",
      productModel: "",
      prodDescription: "",
      prodPrice: "",
      promoPrice: "",

      submitted: {
        productName: "",
        productModel: "",
        prodDescription: "",
        prodPrice: "",
        promoPrice: ""
      },
      inputs: [
        {
          name: "",
          value: ""
        }
      ]
    };
  },
  methods: {
    formSubmit: function(event) {
      ts.productName = this.productName;
      ts.productModel = this.productModel;
      ts.prodDescription = this.prodDescription;
      ts.prodPrice = this.prodPrice;
      ts.promoPrice = this.promoPrice;
      event.target.reset();
    },
    resetForm(e) {
      e.preventDefault();
      this.productName = "";
      this.productModel = "";
      this.prodDescription = "";
      this.prodPrice = "";
      this.promoPrice = "";
      this.inputs = [{ name: "", value: "" }];
      ts.productName = this.productName;
      ts.productModel = this.productModel;
      ts.prodDescription = this.prodDescription;
      ts.prodPrice = this.prodPrice;
      ts.promoPrice = this.promoPrice;
    },
    add(index) {
      this.inputs.push({ name: "", value: "" });
    },
    remove(index) {
      this.inputs.splice(index, 1);
    }
  }
};
</script>

<style></style>
