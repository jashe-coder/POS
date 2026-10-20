<script>

export default {

  data() {
    return {
      allSections: false,
      showFirst: '',

      username: '',
      password: '',

      loggingIn: true,
      logOut: true,
    }
  },
  methods: {
    section(name) {
      this.$emit('goTo', name);
    },

    login() {
      if (this.username === 'jashing' && this.password === '1995') {
        alert('Log in successfully!')
        this.allSections = true;
        this.showFirst = 'Dashboard';
        this.loggingIn = false;
        this.logOut = true;
        this.$emit('login')
      } else {
        alert('Please enter username and password!')
      }
    },

    logout() {
      this.allSections = false;
      this.showFirst = 'Dashboard';
      this.loggingIn = true;
      this.logOut = false;

      this.username = '';
      this.password = '';
    }
  }
}
</script>

<template>
  <div class="overflow-x-hidden">

    <div v-if="allSections" class="w-56 bg-[#302218] text-white p-5 min-h-screen shrink-0 fixed">

      <h1 class="text-2xl font-bold">Bistro Lumière</h1>
      <p class="text-xs mb-10 mt-3">CAFÉ & RESTAURANT</p>

      <p @click="section('Dashboard')" class="block w-full text-left p-3 hover:bg-[#72533c]">Dashboard</p>
      <p @click="section('POS-System')" class="block w-full text-left p-3 hover:bg-[#72533c]">POS System
      </p>

      <p @click="section('Transactions')" class="block w-full text-left p-3 hover:bg-[#72533c]">Transactions
      </p>


      <button v-if="LogIn" @click="section('login')" class="block w-full text-left p-3 hover:bg-[#72533c]">Log
        In</button>

      <div v-if="logOut">
        <p @click="logout" class="block w-full text-left p-3 hover:bg-[#72533c]">Log
          Out</p>
      </div>

    </div>

    <div v-if="loggingIn">
      <div class="bg-[#f8f4ef] p-10 h-screen fixed z-50 w-full">
        <div class="bg-white p-8 rounded-xl shadow mx-auto w-80">
          <h1 class="text-3xl font-bold text-center">Bistro Lumière</h1>
          <p class="text-center mb-6">CAFÉ & RESTAURANT</p>
          <h2 class="text-xl font-bold mb-4">Log In</h2>
          <input v-model="username" placeholder="Username" class="border p-3 w-full mb-3 rounded">
          <input v-model="password" type="password" placeholder="Password" class="border p-3 w-full mb-4 rounded">
          <button @click="login" class="bg-[#302218] text-white p-3 w-full rounded">Log In</button>
        </div>
      </div>
    </div>
  </div>

</template>