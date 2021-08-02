<script>
import Header from "@/components/Header";
import Footer from "@/components/Footer";
import Home from "@/pages/Home";

export default {
  name: 'App',
  components: {
    Header,
    Footer,
    Home
  },
  data() {
    return {
      totalContacts: 0,
    }
  },
  methods: {
    updateTotal(total) {
      this.totalContacts = total;
    }
  }
}
</script>

<template>
  <div id="app" class="page-layout">
    <Header class="container mx-auto px-9 py-2" :total-contacts="totalContacts" />
    <Home class="container mx-auto px-9 py-6" @update-total="updateTotal" />
    <Footer class="container mx-auto px-9 py-4" />
  </div>
</template>


<style>
.page-layout {
  height: 100vh;
  display: grid;
  grid-template-rows: min-content 1fr min-content;
}
</style>
