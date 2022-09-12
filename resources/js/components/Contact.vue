<template>
    <div>
        <div v-for="contact in JSON.parse(JSON.stringify(contacts))">
            <contact-list :contact=contact @edit="showAlert"></contact-list>
        </div>
    </div>
</template>

<script>
export default {
    name: "Contact",
    components: {},

    data() {
        return {
            contacts: {},
        }
    },

    methods: {
        fetchContacts() {
            axios.get("http://127.0.0.1:8000/api/contacts")
                .then(response => {
                    let contactData = JSON.parse(JSON.stringify(response.data));
                    this.contacts = contactData.data;
                    console.log("Contacts are: ");
                    console.log(this.contacts);
                })
        }, //fetchContacts()

        showAlert() {
            alert("Edited");
        } // showAlert()

        // syncContact() {
        //
        // },
        //
        // deleteContact() {
        //
        // },
    }, // methods

    mounted() {
        console.log("Contact Component Mounted");
        this.fetchContacts();
    }
}
</script>
