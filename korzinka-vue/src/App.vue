<template>
  <div class="container">
    <div class="box1">
      <div class="form">
        <div>
          <label>Product name : </label>
          <input type="text" placeholder="product name" v-model="name" />
        </div>
        <div>
          <label>Product hajmi : </label>
          <input type="number" placeholder="product kg" v-model="hajmi" />
        </div>
        <div>
          <label>Product narxi : </label>
          <input type="number" placeholder="product price" v-model="price" />
        </div>
        <div>
          <label>Check product : </label>
          <input type="text" placeholder="check products" v-model="check" />
        </div>
      </div>
      <div class="buttons" @submit.prevent>
        <button @click="addProduct" type="submit" class="btn btn-success btn-sm">
          <i class="fas fa-cart-shopping"></i>
        </button>
        <button type="submit" @click="buyBtn" class="btn btn-primary btn-sm">Buy</button>
        <button type="submit" @click="checkBtn" class="btn btn-warning btn-sm">
          Check
        </button>
        <button type="submit" class="btn btn-danger btn-sm">Reset</button>
      </div>
    </div>
    <div class="box2 d-none" ref="box">
      <div class="box2Items" v-for="product in products">
        <div class="product-img">
          <img :src="`../product-${product.randomNumber}.png`" />
        </div>
        <div class="product-info">
          <div class="productText">
            <h4>Nomi : {{ product.name }}</h4>
            <p>Hajmi : {{ product.hajmi }} kg</p>
            <p>1 kg narxi : {{ product.price }} so'm</p>
            <p>Umumiy narxi : {{ product.hajmi * product.price }} so'm</p>
            <button
              ref="deleteBtn"
              class="btn btn-danger btn-sm"
              @click="onDelete(product.id)"
            >
              Delete
            </button>
          </div>
        </div>
      </div>
    </div>
    <div class="box2" ref="buy">
      <div class="box2Items" v-for="product in products">
        <div class="product-img">
          <img :src="`../product-${product.randomNumber}.png`" />
        </div>
        <div class="product-info">
          <div class="productText">
            <h4>Nomi : {{ product.name }}</h4>
            <p>Hajmi : {{ product.hajmi }} kg</p>
            <p>1 kg narxi : {{ product.price }} so'm</p>
            <p>Umumiy narxi : {{ product.hajmi * product.price }} so'm</p>
          </div>
        </div>
      </div>
    </div>
    <div class="check-message d-none" ref="message">
      <h5 v-for="message in messages" ref="success">{{ message }}</h5>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      name: "",
      hajmi: "",
      price: "",
      id: 1,
      check: "",
      products: [],
      messages: [],
    };
  },
  methods: {
    addProduct() {
      let old_product = this.products.findIndex((obj) => obj.name == this.name);
      if (this.products.findIndex((obj) => obj.name == this.name) == -1) {
        const product = {
          name: this.name,
          hajmi: this.hajmi,
          price: this.price,
          id: this.id++,
          randomNumber: Math.floor(Math.random() * 15 + 1),
        };
        this.products.push(product);
      } else {
        this.products[old_product].hajmi += this.hajmi;
      }
      this.$refs.box.classList.remove("d-none");
      this.$refs.buy.classList.add("d-none");
      this.$refs.message.classList.add("d-none");
      this.check = "";
    },
    onDelete(id) {
      this.products = this.products.filter((obj) => obj.id != id);
    },
    buyBtn() {
      this.$refs.buy.classList.remove("d-none");
      this.$refs.box.classList.add("d-none");
      this.$refs.message.classList.add("d-none");
      this.check = "";
    },
    checkBtn() {
      let checkProduct = this.products.find((obj) => {
        return obj.name.toLowerCase() == this.check.toLowerCase();
      });
      this.$refs.message.classList.remove("d-none");
      this.$refs.buy.classList.add("d-none");
      this.$refs.box.classList.add("d-none");
      if (checkProduct) {
        let succesMessage = `${this.check} tanlangan mahsulotlar ichida mavjud`;
        this.messages.push(succesMessage);
      } else {
        let errorMessage = `${this.check} tanlangan mahsulotlar ichida mavjud emas`;
        this.messages.push(errorMessage);
      }
    },
  },
};
</script>
<style>
body {
  height: 100vh;
  background-image: linear-gradient(to top right, blue, purple, orange);
  background-repeat: no-repeat;
}
.container {
  margin-top: 4rem;
  display: flex;
}
.box1 {
  min-width: 20rem;
}
.box2 {
  margin-left: 2rem;
  display: flex;
  min-height: 10rem;
  border-radius: 0.5rem;
  flex-wrap: wrap;
}
.buttons {
  margin-top: 2rem;
  text-align: center;
}
.buttons button {
  display: block;
  margin-bottom: 0.5rem;
  width: 10rem;
  margin-left: 5rem;
}
.form div {
  margin-bottom: 1rem;
  display: flex;
  justify-content: space-between;
}
.form div label {
  margin-right: 0.5rem;
}
input {
  border-radius: 5px;
  padding: 5px;
}
.product-info {
  display: flex;
  align-items: center;
}
.product-info button {
  align-self: center;
  width: 80%;
}
.product-img img {
  height: 8rem;
}
.product-img {
  display: flex;
  justify-content: center;
  align-self: center;
}
.productText {
  display: flex;
  flex-direction: column;
}
.box2Items {
  margin-left: 1rem;
  margin-right: 1rem;
  margin-bottom: 1rem;
  background-color: white;
  padding: 1rem;
  border-radius: 0.5rem;
}
.check-message {
  margin-left: 2rem;
}
</style>
