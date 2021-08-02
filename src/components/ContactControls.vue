<script>
import Button from "@/components/Button";

export default {
  name: 'ContactControls',
  components: {
    Button
  },
  props: {
    searchValue: {
      type: String,
      required: true
    }
  }
}
</script>

<template>
  <div class="flex flex-col-reverse sm:flex-row justify-between mb-4">
    <div id="search-input-group" class="relative w-full sm:w-96 mb-4">
      <div class="absolute inset-y-0 left-0 pl-4 flex items-center pointer-events-none">
        <i class="fas fa-search text-purple-300 text-lg" aria-hidden="true" />
      </div>
      <input
        type="text"
        name="name"
        placeholder="Search by name"
        class="border rounded-full focus:ring-purple-300 focus:border-purple-300 focus:ring-2 block w-full pl-11 py-1 text-lg border-gray-300 outline-none"
        :value="searchValue"
        @input="e => $emit('update-search-value', e.target.value)"
        autocomplete="off"
      >
    </div>
    <Button @click="$emit('open-add-contact')" class="mb-4">
      <i class="fas fa-plus mr-2" /> Add Contact
    </Button>
  </div>
</template>