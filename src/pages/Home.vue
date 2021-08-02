<script>
import ContactControls from "@/components/ContactControls";
import AddContactModal from "@/components/AddContactModal";
import ContactList from "@/components/ContactList";

export default {
	name: "Home",
	components: {
		ContactControls,
		AddContactModal,
		ContactList,
	},
	data() {
		return {
      searchValue: '',
			isAddContactOpen: false,
			contacts: [
				{
          name: "Jon Snow",
					phone: "1231231231",
					color: "green",
					initials: "JS",
					id: 1627861766350,
				},
				{
          name: "Arya Stark",
					phone: "2423423523",
					color: "red",
					initials: "AS",
					id: 1627861781924,
				},
				{
          name: "Joshua Martinez",
					phone: "7863516544",
					color: "green",
					initials: "JM",
					id: 1627861795807,
				},
				{
          name: "Selina Kyle",
					phone: "9879879873",
					color: "purple",
					initials: "SK",
					id: 1627861810759,
				},
				{
          name: "Bruce Wayne",
					phone: "9872342423",
					color: "red",
					initials: "BW",
					id: 1627861825248,
				},
				{
          name: "Leonardo Dicaprio",
					phone: "3120980980",
					color: "blue",
					initials: "LD",
					id: 1627861863443,
				},
				{
          name: "Kate Winslet",
					phone: "5833098404",
					color: "blue",
					initials: "KW",
					id: 1627861891109,
				},
				{
          name: "Lebron James",
					phone: "7872344234",
					color: "blue",
					initials: "LJ",
					id: 1627861918030,
				},
				{
          name: "Serena Williams",
					phone: "9892342424",
					color: "purple",
					initials: "SW",
					id: 1627861932238,
				},
				{
          name: "Bruno Mars",
					phone: "4242423423",
					color: "red",
					initials: "BM",
					id: 1627861967379,
				},
				{
          name: "Sade Adu",
					phone: "2342342342",
					color: "purple",
					initials: "SA",
					id: 1627861990099,
				},
			],
		};
	},
  mounted() {
    this.$emit("update-total", this.contacts.length);
  },
	watch: {
		contacts(newValue, oldValue) {
			if (newValue.length !== oldValue.length) {
				this.$emit("update-total", newValue.length);
			}
		},
	},
  computed: {
    filteredContacts() {
      return this.contacts.filter(contact => contact.name.toLowerCase().includes(this.searchValue));
    }
  },
	methods: {
    updateSearchValue(value) {
      this.searchValue = value;
    },
		addContact(contact) {
			this.contacts = [...this.contacts, contact];
		},
		deleteContact(contactId) {
			this.contacts = this.contacts.filter(
				(contact) => contact.id !== contactId
			);
		},
	},
};
</script>

<template>
  <div>
    <ContactControls 
      :search-value="searchValue"
      @update-search-value="updateSearchValue"
      @open-add-contact="isAddContactOpen = true"
    />
    <ContactList 
      :contacts="filteredContacts"
      @delete="deleteContact"
    />
    <AddContactModal 
      :is-open="isAddContactOpen"
      @close="isAddContactOpen = false"
      @save-contact="addContact"
    />
  </div>
</template>