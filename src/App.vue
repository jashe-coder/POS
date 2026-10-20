<script>
import LogIn from './components/LogIn.vue'
import Sidebar from './components/Sidebar.vue'
import POS from './components/POS.vue'
import Transactions from './components/Transactions.vue'
import Dashboard from './components/Dashboard.vue'


export default {
  components: {
    LogIn,
    Sidebar,
    POS,
    Transactions,
    Dashboard,

  },

  data() {
    return {
      foods: [
        { id: 1, name: 'Smokin’ Cheese ', price: 7, image: 'https://i.pinimg.com/736x/b0/26/c2/b026c24ca17443864fc197de6e4d6450.jpg' },
        { id: 2, name: 'Smoked Pepperoni Ember ', price: 10, image: 'https://i.pinimg.com/1200x/d8/41/68/d841683564febc4860a504b1861c869a.jpg' },
        { id: 3, name: 'Spicy Inferno Glaze', price: 8, image: 'https://i.pinimg.com/736x/97/be/97/97be9743f70d89962d4079e0b832eb74.jpg' },
        { id: 4, name: 'Quesadilla Italiano', price: 5, image: 'https://i.pinimg.com/1200x/ee/65/aa/ee65aaf5b150fb2bb0d169ecc70802f0.jpg' },
        { id: 5, name: 'Wagyu Steak ', price: 15, image: 'https://i.pinimg.com/236x/ae/cb/3f/aecb3fbd900b855acab384762bc83f6e.jpg' },
        { id: 6, name: 'Radiatori', price: 9, image: 'https://i.pinimg.com/1200x/ef/3a/43/ef3a437e2d45bf192498ded31c0aee66.jpg' },
        { id: 7, name: 'Cluckin’ Good BBQ', price: 11, image: 'https://i.pinimg.com/1200x/5d/80/99/5d809934efcaf583c99ea57ba76f8c62.jpg' },
        { id: 8, name: 'Khao Phat Green Carrot', price: 6, image: 'https://i.pinimg.com/1200x/42/12/0c/42120cdfbc28e69c3e7c3646ee9609bd.jpg' },
        { id: 9, name: 'Rice', price: 4, image: 'https://i.pinimg.com/1200x/0c/38/78/0c3878e91ca39ef98c58bf19fb49c476.jpg' },
        { id: 10, name: 'Decadent Shakes', price: 4, image: 'https://i.pinimg.com/736x/52/48/ce/5248cea69ba1a478f1b7484bcbb06784.jpg' },
        { id: 11, name: 'Fresh Cucumber Juice', price: 3, image: 'https://i.pinimg.com/1200x/03/9a/21/039a214c8298c96e26c0cf10621c3939.jpg' },
        { id: 12, name: 'Thé glacé', price: 3, image: 'https://i.pinimg.com/736x/a6/f4/f7/a6f4f7c3f6042346b198e9f2001bcdb3.jpg' },
      ],
      page: 'Dashboard',
      orders: [],
      angFoods: null,
      foodLength: ''
    }
  },
  methods: {
    changePage(name) {
      this.page = name
    },

    saveOrder(order) {
      this.orders.push(order)
    },
    pushSaFoods(id, name, price, image) {
      this.foods.push({ ...id, ...name, ...price, ...image });
    },
    paraSalength(i) {
      this.foodLength = i
    }
  },
  mounted() {
    this.foodLength = this.foods.length
  },
}
</script>

<template>
  <div class="flex">

    <Sidebar @goTo="changePage" />

    <div class="w-full p-6 ml-53">

      <LogIn v-if="page === 'Login'" @login="LogIn" />

      <POS @totalPrice="TotalP" v-if="page === 'POS-System'" @saveOrder="saveOrder" :foodArray="foods"
        @addFood="pushSaFoods" @foodsLength="paraSalength" />

      <Transactions v-if="page === 'Transactions'" :orders="orders" />

      <Dashboard v-if="page === 'Dashboard'" :orders="orders" @goTo="changePage" :gipasaAngLength="this.foodLength" />

    </div>

  </div>
</template>
