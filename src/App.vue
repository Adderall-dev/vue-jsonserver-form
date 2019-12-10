<template>
  <div id="app">
    <h1>SIMPLE FORM</h1>
    <form id="form" @submit.prevent="addToAPI">
      <br /><br />
      <input v-model.lazy="productName" placeholder="nazwa produktu" />
      <br /><br />
      <input v-model.trim="productModel" placeholder="model produktu" />
      <br /><br />
      <textarea v-model.trim="prodDescription" placeholder="opis"></textarea>
      <br /><br />
      <input v-model.number="prodPrice" type="number" placeholder="cena" />
      <br /><br />
      <input
        v-model.number="promoPrice"
        type="number"
        placeholder="cena promocyjna"
      />
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
      <button>SUBMIT</button><span></span>
      <button @click="resetForm">RESET</button>
    </form>
    <br /><br />
    <div>
      <h3>Wprowadzone Dane:</h3>
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
import axios from "axios";

export default {
  name: "app",
  data() {
    return {
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
    addToAPI(e) {
      let newFormData = {
        productName: this.productName,
        productModel: this.productModel,
        prodDescription: this.prodDescription,
        prodPrice: this.prodPrice,
        promoPrice: this.promoPrice,
        inputs: [{ name: "", value: "" }]
      };
      console.log(newFormData);
      e.target.reset();
    },
    resetForm(e) {
      e.preventDefault();
      this.productName = "";
      this.productModel = "";
      this.prodDescription = "";
      this.prodPrice = "";
      this.promoPrice = "";
      this.inputs = [{ name: "", value: "" }];
      this.submitted.productName = this.productName;
      this.submitted.productModel = this.productModel;
      this.submitted.prodDescription = this.prodDescription;
      this.submitted.prodPrice = this.prodPrice;
      this.submitted.promoPrice = this.promoPrice;
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

<style scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  text-align: center;
}
h3 {
  color: #768bad;
}
h1 {
  color: #768bad;
}
textarea {
  border: 0;
  outline: 0;
  border-left: 2px solid #768bad;
  font-size: 1.2em;
  background-color: #d3dded;
}
textarea:focus {
  border: 0;
  border-bottom: 2px solid #768bad;
}
input {
  border: 0;
  outline: 0;
  font-size: 1em;
  border-left: 2px solid #768bad;
  padding: 4px;
  background-color: #d3dded;
  border-radius: 4px;
}
input:focus {
  border: 0;
  border-bottom: 2px solid #768bad;
}
button {
  background-color: #a7b8d4;
  border: 1px solid#9babc4;
  color: white;
  height: 30px;
  width: 100px;
  border-radius: 4px;
}
button:hover {
  background-color: #626e80;
  cursor: pointer;
}
span {
  padding: 4px;
}
</style>
