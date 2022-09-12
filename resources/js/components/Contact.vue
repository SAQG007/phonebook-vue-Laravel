<template>
    <div>
        <form v-on:submit.prevent="addNewContact()">
            <div>
                <input type="text" name="name" v-model="formData.name" placeholder="Name">
            </div>
            <div>
                <input type="text" name="phone" v-model="formData.phone" placeholder="Phone">
            </div>
            <div>
                <input type="text" name="email" v-model="formData.email" placeholder="Email">
            </div>
            <div>
                <button class="btn btn-success active">Add New Contact</button>
            </div>
        </form>
        <div v-for="contact in contacts"> <!--contact in JSON.parse(JSON.stringify(contacts))-->
            <contact-list :contact=contact @edit="showAlert" @deleteContact="deleteContact"></contact-list>
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
            formData: {
                name: "",
                phone: "",
                email: "",
            },
        }
    },

    methods: {
        fetchContacts() {
            // axios.get("http://127.0.0.1:8000/api/contacts")
            axios.get(window.baseUrl + "contacts")
                .then(response => {
                    let contactData = JSON.parse(JSON.stringify(response.data));
                    this.contacts = contactData.data;
                    console.log("Contacts are: ");
                    console.log(this.contacts);
                })
        }, //fetchContacts()

        addNewContact() {
            axios.post(window.baseUrl + "contact", this.formData)
                .then(response => {
                    console.log(response)
                })
                .catch(error => {
                    console.log(error)
                });
        },

        showAlert(value) {
            alert(value);
        }, // showAlert()

        deleteContact(value) {
            console.log("http://127.0.0.1:8000/api/contact/" + value);
            axios.delete("http://127.0.0.1:8000/api/contact/" + value)
                .then(response => {
                    console.log("Contact Deleted");
                    console.log(response);
                })
                .catch(error => {
                    console.log("Unable to delete contact");
                    console.log(error);
                });
        }, // deleteContact()

        // syncContact() {
        //
        // },

    }, // methods

    mounted() {
        console.log("Contact Component Mounted");
        this.fetchContacts();
    }
}
</script>
