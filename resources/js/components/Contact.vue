<template>
    <div>
        <div v-for="contact in contacts">
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
            contacts: [],
        }
    },

    methods: {
        fetchContacts() {
            this.contacts = [
                {
                    'id': '1',
                    'name': 'Ali',
                    'phone': '11111111',
                    'email': 'ali@example.com'
                },
                {
                    'id': '2',
                    'name': 'Ahmed',
                    'phone': '2222222',
                    'email': 'ahmed@example.com'
                },
            ]

           // axios.get('http://127.0.0.1:8000/api/contacts')
           //     .then(function (response) {
           //         this.contacts = response.data;
           //     });
        }, // fetchContacts

        showAlert() {
            alert("Edited");
        } // showAlert

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
