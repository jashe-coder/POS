<script>
export default {
  props: ['foodArray'],
  data() {
    return {
      // foods: [
      //   { id: 1, name: 'Smokin’ Cheese ', price: 7, image: 'https://i.pinimg.com/736x/b0/26/c2/b026c24ca17443864fc197de6e4d6450.jpg' },
      //   { id: 2, name: 'Smoked Pepperoni Ember ', price: 10, image: 'https://i.pinimg.com/1200x/d8/41/68/d841683564febc4860a504b1861c869a.jpg' },
      //   { id: 3, name: 'Spicy Inferno Glaze', price: 8, image: 'https://i.pinimg.com/736x/97/be/97/97be9743f70d89962d4079e0b832eb74.jpg' },
      //   { id: 4, name: 'Quesadilla Italiano', price: 5, image: 'https://i.pinimg.com/1200x/ee/65/aa/ee65aaf5b150fb2bb0d169ecc70802f0.jpg' },
      //   { id: 5, name: 'Wagyu Steak ', price: 15, image: 'https://i.pinimg.com/236x/ae/cb/3f/aecb3fbd900b855acab384762bc83f6e.jpg' },
      //   { id: 6, name: 'Radiatori', price: 9, image: 'https://i.pinimg.com/1200x/ef/3a/43/ef3a437e2d45bf192498ded31c0aee66.jpg' },
      //   { id: 7, name: 'Cluckin’ Good BBQ', price: 11, image: 'https://i.pinimg.com/1200x/5d/80/99/5d809934efcaf583c99ea57ba76f8c62.jpg' },
      //   { id: 8, name: 'Khao Phat Green Carrot', price: 6, image: 'https://i.pinimg.com/1200x/42/12/0c/42120cdfbc28e69c3e7c3646ee9609bd.jpg' },
      //   { id: 9, name: 'Rice', price: 4, image: 'https://i.pinimg.com/1200x/0c/38/78/0c3878e91ca39ef98c58bf19fb49c476.jpg' },
      //   { id: 10, name: 'Decadent Shakes', price: 4, image: 'https://i.pinimg.com/736x/52/48/ce/5248cea69ba1a478f1b7484bcbb06784.jpg' },
      //   { id: 11, name: 'Fresh Cucumber Juice', price: 3, image: 'https://i.pinimg.com/1200x/03/9a/21/039a214c8298c96e26c0cf10621c3939.jpg' },
      //   { id: 12, name: 'Thé glacé', price: 3, image: 'https://i.pinimg.com/736x/a6/f4/f7/a6f4f7c3f6042346b198e9f2001bcdb3.jpg' },
      // ],
      carts: [],
      total: 0,
      overAllTotal: 0,
      cash: '',
      showAdd: false,
      productName: '',
      productPrice: '',
      productImage: ''
    }
  },
  computed: {
    change() {
      return (this.cash) - this.total
    }
  },
  methods: {
    addToCart(food) {
      this.carts.push(food)
      this.total += food.price
    },
    removeItem(index) {
      this.total -= this.carts[index].price
      this.carts.splice(index, 1)
    },
    cancel() {
      this.productName = '',
        this.productPrice = '',
        this.productImage = '',
        this.showAdd = false
    },
    addProduct() {
      if (this.productName != '' && Number(this.productPrice) > 0) {
        this.$emit('addFood', {
          id: this.foodArray.length + 1,
          name: this.productName,
          price: Number(this.productPrice),
          image: this.productImage
        })
        this.$emit('foodsLength', this.foodArray.length)
        console.log(this.foodArray.length)
        alert('Product added successfully!')
        this.productName = ''
        this.productPrice = ''
        this.productImage = ''
        this.showAdd = false
      } else {
        alert('Please enter product name and price!')
      }

    },

    placeOrder() {
      if (this.carts.length === 0) {
        alert('Please select food!')
      } else if (!this.cash || Number(this.cash) < this.total) {
        alert('Insufficient payment!')
      } else {
        this.$emit('saveOrder', {
          items: this.carts.length,
          total: this.total
        })
        alert('Order Successful! Change: $' + (Number(this.cash) - this.total))
        this.carts = []
        this.total = 0
        this.cash = ''
      }
    }
  }
}
</script>

<template>
  <div class="w-full">
    <h1 class="text-3xl font-bold mb-5">POS System</h1>
    <button @click="showAdd = !showAdd" class="bg-[#302218] text-white p-3 rounded mb-5">+ Add Product</button>
    <div v-if="showAdd" class="bg-white p-5 rounded-xl shadow mb-5">
      <h2 class="text-xl font-bold mb-4">Add New Product</h2>
      <input v-model="productName" placeholder="Product Name" class="border p-3 w-150 mb-3 rounded">
      <input v-model="productPrice" type="number" placeholder="Price" class="border p-3 w-150 mb-3 rounded">
      <input v-model="productImage" placeholder="images" class="border p-3 w-150 mb-3 rounded">
      <div class="flex gap-5">
        <button @click="addProduct" class="bg-[#302218] text-white p-3 rounded">Save Product</button>
        <button @click="cancel" class="bg-[#302218] text-white p-3 rounded cursor-pointer">Cancel</button>
      </div>

    </div>
    <div class="flex gap-5 justify-center">
      <!-- FOOD MENU -->
      <div class="w-3/4 max-h-116 overflow-y-scroll">
        <h2 class="text-xl font-bold mb-4">Food Menu</h2>
        <div class="grid grid-cols-3 gap-4 w-180">
          <div v-for="food in foodArray" :key="food.id"
            class="bg-white p-4 rounded-xl shadow text-center border border-black">
            <img :src="food.image" alt="" class="w-full h-40 mb-5 rounded-md object-cover cursor-pointer">
            <h3 class="font-bold">{{ food.name }}</h3>
            <p class="my-2">${{ food.price }}</p>
            <button @click="addToCart(food)" class="bg-[#302218] text-white px-4 py-2 rounded-md cursor-pointer">
              Add to Cart
            </button>
          </div>
        </div>
      </div>
      <!-- CURRENT ORDER -->
      <div class="bg-white p-5 rounded-xl shadow border border-black">
        <h2 class="text-xl font-bold mb-4">Current Order</h2>
        <p v-if="carts.length === 0">No items selected.</p>
        <div v-for="(item, index) in carts" :key="index" class="border-b py-3">
          <p>{{ item.name }}</p>
          <p>${{ item.price }}</p>
          <button @click="removeItem(index)" class="text-red-600">Cancel</button>
        </div>
        <h2 class="text-xl font-bold mt-5">Total: ${{ total }}</h2>
        <p class="mt-4">Cash Payment:</p>
        <input type="number" v-model.number="cash" class="border p-2 w-full rounded" placeholder="Enter cash">
        <p class="mt-4">Change: ${{ change >= 0 ? change : 0 }}</p>
        <button @click="placeOrder" class="bg-[#302218] text-white p-3 w-full rounded mt-4">Pay</button>
      </div>
    </div>

  </div>
</template>