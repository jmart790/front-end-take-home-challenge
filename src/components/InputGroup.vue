<script>
export default {
  name: 'InputGroup',
  props: {
    name: {
      type: String,
      required: true
    },
    label: {
      type: String,
      required: true
    },
    value: {
      type: String,
      required: true,
    },
    placeholder: {
      type: String,
      default: '',
    },
    invalid: {
      type: Boolean,
      default: false,
    },
    success: {
      type: Boolean,
      default: false,
    },
    feedback: {
      type: String,
      default: '',
    },
  }
}
</script>

<template>
  <div>
    <label for="Name" class="block text-sm font-medium text-gray-700">{{ label }}</label>
    <div class="mt-1 relative">
      <input
        type="text"
        :name="name"
        :value="value"
        v-bind="$attrs"
        v-on="{ ...$listeners, input: event => $emit('input', event.target.value) }"
        :placeholder="placeholder"
        class="shadow-sm border px-4 py-2  focus:border-purple-300 block w-full sm:text-sm border-gray-300 rounded-md outline-none focus:ring-2 focus:ring-purple-300"
        :class="{
          'border-red-300 focus:outline-none focus:ring-red-500 focus:border-red-500 pr-11': invalid,
          'border-green-300 focus:outline-none focus:ring-green-500 focus:border-green-500 pr-11': success
        }"
      >
      <div v-show="invalid" class="absolute inset-y-0 right-0 pr-4 flex items-center pointer-events-none">
        <i class="text-lg fas fa-exclamation-circle text-red-500" />
      </div>
      <div v-show="success" class="absolute inset-y-0 right-0 pr-4 flex items-center pointer-events-none">
        <i class="text-lg fas fa-check-circle text-green-500" />
      </div>
    </div>
    <p v-if="invalid" class="mt-2 text-sm text-red-600">
      {{ feedback }}
    </p>
  </div>
</template>