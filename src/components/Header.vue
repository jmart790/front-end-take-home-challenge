<script>
  export default {
    name: 'Header',
    props: {
      totalContacts: {
        type: Number,
        required: true
      }
    }
  }
</script>

<template>
  <div class="border-b-2 flex justify-between items-center">
    <h2 class="font-semibold text-xl">
      All Contacts ({{ totalContacts }})
    </h2>
    <img class="h-12 w-12 rounded-full" src="../assets/images/bonzaiYoshProfilePic.jpg" alt="Profile Picture">
  </div>    
</template>