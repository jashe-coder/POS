<script>
export default {
  props: ['orders']
}
</script>

<template>
  <div class="w-full">
    <h1 class="text-3xl font-bold mb-5">Transactions</h1>

    <div class="bg-white p-5 rounded-xl shadow">
      <h2 class="text-xl font-bold mb-4">Order History</h2>
      <p v-if="orders.length == 0">No transactions yet.</p>
      <table v-else class="w-full text-left">
        <thead>
          <tr class="border-b">
            <th class="p-3">Order No.</th>
            <th class="p-3">Items</th>
            <th class="p-3">Total</th>
            <th class="p-3">Status</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(order, index) in orders":key="index"class="border-b">
            <td class="p-3">#{{ index + 1 }}</td>

            <td class="p-3">{{ order.items }}</td>

            <td class="p-3">${{ order.total }}</td>

            <td class="p-3 text-green-800">Completed</td>
          </tr>
        </tbody> 
      </table>
    </div>
  </div>
</template>