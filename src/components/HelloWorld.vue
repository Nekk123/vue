<template>
  <div>
    <div class="container mt-4">
      <div class="row">

        <div class="col-md-6">
          <div class="product-image left-image">
            <img v-bind:src="require('../assets/' + image)" 
            alt="test">
          </div>  
        </div>

        <div class="col-md-6">
          <div class="product-info">
            <h1>Product: {{ title }}</h1>
            <p v-if="inventory > 10">In Stock</p>
            <p v-else-if="inventory <= 10 && inventory > 0">
              Almost sold out!
            </p>
            <p v-else>Out of Stock</p>

            <ul>
              <li v-for="detail in details">{{ detail }}</li>
            </ul>

            <div v-for="varian in varians" 
                :key="varian.varianId"
                class="color-box"
                :style="{ backgroundColor: varian.variantColoror }"
                @mouseover="updateProduct(varian.variantImage)">
            </div>

            <button v-on:click="addToCart" 
             :disabled="!inventory"
             :class="{ disabledButton: !inventory }"
             class="btn btn-primary mb-3 mt-3">Add to Car</button>

            <div class="cart">
              <p>Cart({{cart}})</p>
            </div>

          <formfiels></formfiels>

          </div>
        </div>

      </div>
    </div>
   </div>



</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      brand: 'Vue Master',
      product: 'socks',
      image: 'sock.jpeg',
      inventory: 100,
      details: ["80% cotton", "20% polyester", "Gender-neutral"],
      varians: [
        {
          varianId: 2234,
          variantColoror: "green",
          variantImage: 'sock.jpeg'
        },
        {
          varianId: 2235,
          variantColoror: "blue",
          variantImage: 'bluesock.jpeg'
        }
      ],
      cart: 0
    }
  },
  methods: {
    addToCart() {
      this.cart += 1
    },
    updateProduct(variantImage) {
      this.image = variantImage
    }
  },
  computed: {
    title() {
      return this.brand + ' ' + this.product
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .left-image img{
    width: 50%;
  }

  .color-box{
    width: 40px;
    height: 40px;
    margin-top: 5px;
  }

  .disabledButton{
    background-color: gainsboro;
    border: none;
  }
</style>
