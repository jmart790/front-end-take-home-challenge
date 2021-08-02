<script>
export default {
  name: 'Button',
  props: {
    type: {
      type: String,
      default: 'button'
    },
    variant: {
      type: String,
      default: 'primary'
    },
    isRound: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    buttonClass() {
      if (this.variant === 'secondary') {
        return 'border border-gray-300 bg-white text-base font-medium text-gray-500 hover:text-gray-700'
      }
      else if (this.variant === 'danger') {
        return 'bg-red-500 hover:bg-red-700 text-white font-semibold'
      }
      else if (this.variant === 'terciary') {
        return 'hover:bg-gray-100 text-gray-500 hover:text-gray-700 font-semibold'
      }
      return 'bg-purple-500 hover:bg-purple-700 text-white font-semibold'
    }
  }
}
</script>

<template>
  <button 
    :type="type"
    class="py-2 px-6 inline-flex justify-center items-center rounded-full focus:outline-none focus:ring-2  focus:ring-purple-300"
    :class="[buttonClass, {'h-12 w-12 p-0': isRound}]"
    v-on="$listeners"
    v-bind="$attrs"
  >
    <slot />
  </button>  
</template>