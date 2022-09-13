<template>
    <div class="card mt-4 mb-4" style="width: 100%; padding: 10px;" v-if="!isCanceling">
        <h5>Contact Edit Form</h5>
        <div class="card-body">
            <form v-on:submit.prevent="updateContact()">
                <div class="mt-2">
                    <div style="display: inline-block; width: 10%">Name: </div>
                    <div style="display: inline-block"><input type="text" v-model=formData.name></div>
                </div>
                <div class="mt-2">
                    <div style="display: inline-block; width: 10%">Phone: </div>
                    <div style="display: inline-block"><input type="text" v-model=formData.phone></div>
                </div>
                <div class="mt-2">
                    <div style="display: inline-block; width: 10%">Email: </div>
                    <div style="display: inline-block"><input type="text" v-model=formData.email></div>
                </div>

                <div class="mt-4">
                    <button type="submit" class="btn btn-primary active" :disabled="isSaving || isCanceling">{{ saveBtnText }}</button>
                </div>
            </form>
            <button class="btn btn-danger active" @click="toggleIsCanceling()" :disabled="isSaving || isCanceling">{{ cancelBtnText }}</button>
        </div>
    </div>
    <div v-else>
        <contact-list :contact=contactCopy :is-expanded-prop=true></contact-list>
    </div>
</template>

<script>
export default {
    name: "ContactForm",

    data() {
        return {
            isSaving: false,
            isCanceling: false,
            saveBtnText: 'Save',
            cancelBtnText: 'Cancel',
            contactCopy: [],

            formData: {
                id: this.contact.id,
                name: this.contact.name,
                phone: this.contact.phone,
                email: this.contact.email,
            },
        }
    },

    props: {
        contact: {
            require: true,
        },
    },

    methods: {
        toggleIsSaving() {
            this.isSaving = !this.isSaving;
            this.saveBtnText = "Saving";
            this.updateContact();
        },

        toggleIsCanceling() {
            this.isCanceling = !this.isCanceling;
            this.cancelBtnText = "Canceling";
        },

        updateContact() {
            console.log(this.formData.name);
            console.log(window.baseUrl + "contact/" + this.formData.id);
            axios.put(window.baseUrl + "contact/" + this.formData.id, this.formData)
                .then(response => {
                    console.log(response)
                })
                .catch(error => {
                    console.log(error)
                });
            this.isCanceling = !this.isCanceling;
            this.contactCopy = this.formData;
        },

        copyContact() {
            this.contactCopy = this.contact;
        }
    },

    mounted() {
        this.copyContact();
    }
}
</script>
