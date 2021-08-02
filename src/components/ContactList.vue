<script>
import Button from "@/components/Button";

export default {
	name: "ContactList",
	components: {
		Button,
	},
	props: {
		contacts: {
			type: Array,
			required: true,
		},
	},
	methods: {
		formatPhone(phone) {
			if (phone) {
				let x = phone.replace(/\D/g, "").match(/(\d{0,3})(\d{0,3})(\d{0,4})/);
				return !x[2]
					? x[1]
					: "(" + x[1] + ") " + x[2] + (x[3] ? "-" + x[3] : "");
			}
			return "";
		},
    callContact(phone) {
      window.open(`tel:${phone}`);
    }
	},
};
</script>

<template>
  <ul class="contacts-container max divide-y divide-gray-200">
    <li v-for="contact in contacts" :key="contact.id" class="contact">
      <div class="mr-4 h-9 w-9 sm:h-12 sm:w-12 rounded-full uppercase flex items-center place-content-center text-white" :class="`bg-${contact.color}-400`">
        {{ contact.initials }}
      </div>
      <div>
        <p class="text-sm font-medium text-gray-900 capitalize">
          {{ contact.name }}
        </p>
        <p class="block md:hidden text-sm text-gray-500">
          {{ formatPhone(contact.phone) }}
        </p>
      </div>
      <p class="hidden md:block text-sm text-gray-500">
        {{ formatPhone(contact.phone) }}
      </p>
      <Button 
        variant="terciary"
        :is-round="true"
        @click="callContact(contact.phone)"
      >
        <i class="fas fa-phone text-purple-300" />
      </Button>
      <Button 
        variant="terciary"
        :is-round="true"
        class="hidden md:inline-flex"
      >
        <i class="fas fa-comment text-blue-300" />
      </Button>
      <Button 
        variant="terciary"
        :is-round="true"
        @click="$emit('delete', contact.id)"
      >
        <i class="fas fa-trash-alt text-red-300" />
      </Button>
    </li>
  </ul>  
</template>


<style>
.contacts-container {
  max-height: 60vh;
  height: 100%;
	overflow-y: auto;
  padding-right: 1rem;
}
.contacts-container::-webkit-scrollbar-track {
	-webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
	background-color: #F5F5F5;
	border-radius: 10px;
}

.contacts-container::-webkit-scrollbar {
	width: 10px;
	background-color: #F5F5F5;
}

.contacts-container::-webkit-scrollbar-thumb {
	border-radius: 10px;
	background-image: -webkit-gradient(
		linear,
		left bottom,
		left top,
		color-stop(0.44, #C4B5FD),
		color-stop(0.72, #8B5CF6),
		color-stop(0.86, #6D28D9)
	);
}

.contact {
	display: grid;
	align-items: center;
  grid-template-columns: min-content 1fr min-content min-content;
	gap: 1rem;
	padding: 1rem 0;
}
@media screen and (min-width: 768px) { 
  .contacts-container {
    max-height: 70vh;
    padding-right: 2rem;
  }
  .contact {
    grid-template-columns: min-content 200px 1fr min-content min-content min-content;
  }
}
</style>