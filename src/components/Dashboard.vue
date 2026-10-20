<script>
export default {
  props: ['gipasaAngLength', 'orders'],
  mounted() {
    this.gipasaAngLength
  },
  methods: {

    totalSales() {
      return this.orders.reduce((sum, order) => sum + (Number(order.total) || 0), 0)
    },

    newOrder() {
      this.$emit('goTo', 'POS System')
    }
  },

}
</script>

<template>
  <div>
    <h1 class="text-3xl font-bold mb-3">Dashboard</h1>
    <p class="mb-6 text-amber-950 italic font-semibold">
      WELCOME TO Bistro Lumière!
    </p>

    <div class="grid grid-cols-3 gap-4">
      <!-- Total Sales -->
      <div class="bg-white p-6 rounded-xl shadow">
        <p>Total Sales</p>
        <h2 class="text-2xl font-bold">${{ totalSales() }}</h2>
      </div>

      <!-- Total Orders -->
      <div class="bg-white p-6 rounded-xl shadow">
        <p>Total Orders</p>
        <h2 class="text-2xl font-bold">{{ orders.length }}</h2>
      </div>

      <!-- Menu Items -->
      <div class="bg-white p-6 rounded-xl shadow">
        <p>Menu Items</p>
        <h2 class="text-2xl font-bold">{{ gipasaAngLength }}</h2>
      </div>
    </div>

    <div class="bg-white p-6 rounded-xl shadow mt-6">
      <h2 class="text-xl font-bold mb-3">Quick Order</h2>
      <button @click="newOrder"
        class="bg-[#302218] text-white p-3 rounded-md cursor-pointer hover:opacity-90 transition">
        Create New Order
      </button>
    </div>
  </div>
</template>