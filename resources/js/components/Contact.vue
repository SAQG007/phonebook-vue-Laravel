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
                id: "",
                name: "Sample Name",
                phone: "",
                email: "",
            },
        }
    },

    methods: {
        fetchContacts() {
            axios.get(window.baseUrl + "contacts")
                .then(response => {
                    let contactData = JSON.parse(JSON.stringify(response.data));
                    this.contacts = contactData.data;
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
            alert(value.name);
        }, // showAlert()

        deleteContact(value) {
            axios.delete( window.baseUrl + "contact/" + value)
                .then(response => {
                    console.log(response);
                })
                .catch(error => {
                    console.log(error);
                });
        }, // deleteContact()

    }, // methods

    mounted() {
        this.fetchContacts();
    }
}
</script>
