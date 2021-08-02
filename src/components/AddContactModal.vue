<script>
import { required, numeric, minLength, maxLength } from 'vuelidate/lib/validators';
import Button from '@/components/Button';
import InputGroup from '@/components/InputGroup';
const isName = (value) => /^[a-zA-Z ]*$/.test(value);

export default {
	name: "AddContactModal",
  components: {
    Button,
    InputGroup
  },
	props: {
		isOpen: {
			type: Boolean,
			required: true,
		},
	},
  data() {
    return {
      form: {
        name: '',
        phone: '',
        id: ''
      }
    }
  },
  validations: {
    form: {
      name: {
        required,
        isName
      },
      phone: {
        required,
        numeric,
        minLength: minLength(10),
        maxLength: maxLength(10)
      }
    }
  },
  methods: {
    getInitials(name) {
      const splitName = name.split(' ');
      const firstInitial = splitName[0].charAt(0);
      const lastInitial = splitName[splitName.length -1].charAt(0);
      return `${firstInitial}${lastInitial}`;
    },
    getAvatarColor(name) {
      const letter = name.charAt(0).toLowerCase();
      if (letter < 'c') return 'red';
      else if (letter < 'g') return 'yellow';
      else if (letter < 'k') return 'green';
      else if (letter < 'o') return 'blue';
      else if (letter < 'r') return 'indigo';
      else if (letter < 'v') return 'purple';
      else if (letter <= 'z') return 'pink';
      else return 'gray'
    },
    handleSubmit(form) {
      this.$v.form.$touch();
      if (!this.$v.form.$invalid) {
        const initials = this.getInitials(form.name);
        const color = this.getAvatarColor(form.name);
        const contact = {...form, initials, color, id: Date.now() }
        this.$emit('save-contact', contact)
        this.closeForm();
      }
    },
    closeForm() {
      this.$emit('close');
      this.form = {
        name: '',
        phone: '',
        id: ''
      };
      this.$v.form.$reset();
    }
  }
};
</script>

<template>
  <transition name="slide-fade">
    <div 
      v-if="isOpen"
      class="fixed z-10 inset-0 overflow-y-auto" 
      style="top:-2rem;"
      aria-labelledby="modal-title" 
      role="dialog" 
      aria-modal="true"
    >
      <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
        <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" aria-hidden="true" />  
        <!-- This element is to trick the browser into centering the modal contents. -->
        <span class="hidden sm:inline-block sm:align-middle sm:h-screen" aria-hidden="true">&#8203;</span>

        <section class="inline-block align-bottom bg-white rounded-lg px-9 pt-8 pb-7 text-left overflow-hidden shadow-xl transform transition-all sm:align-middle sm:max-w-lg sm:w-full border border-gray-100">
          <h3 class="text-lg leading-6 font-medium text-gray-900">
            Add Contact
          </h3>
          <div class="hidden sm:block absolute top-0 right-0 pt-4 pr-4">
            <button 
              @click.prevent="closeForm"
              class="bg-white rounded-full w-5 h-5 flex items-center justify-center text-xl text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-purple-300"
            >
              <i class="fas fa-times" />
            </button>
          </div>

          <form @submit.prevent="handleSubmit(form)">
            <div class="mt-4">
              <InputGroup 
                label="Name"
                name="Name"
                v-model.trim="form.name"
                placeholder="John Snow"
                @blur="form.name && $v.form.name.$touch()"
                :invalid="$v.form.name.$error"
                :success="!$v.form.name.$error && $v.form.name.$dirty "
                :feedback="!$v.form.name.isName ? 'Please enter alphabet characters only' : 'Name is required'"
                class="mb-4"
              />
              <InputGroup 
                label="Phone Number"
                name="Phone"
                v-model.trim="form.phone"
                maxlength="10"
                placeholder="(xxx) xxx-xxxx"
                @blur="form.phone && $v.form.phone.$touch()"
                :invalid="$v.form.phone.$error"
                :success="!$v.form.phone.$error && $v.form.phone.$dirty "
                :feedback="!$v.form.phone.numeric ? 'Please enter numeric characters only' : '10 digit phone number is required'"
              />
            </div>
            <div class="mt-8 flex flex-row-reverse">
              <Button type="submit" class="ml-4">
                + Add
              </Button>
              <Button @click.prevent="closeForm" variant="secondary">
                Cancel
              </Button>
            </div>
          </form>
        </section>
      </div>
    </div>
  </transition>
</template>

<style>
.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .3s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to {
  transform: translateY(20px);
  opacity: 0;
}
</style>