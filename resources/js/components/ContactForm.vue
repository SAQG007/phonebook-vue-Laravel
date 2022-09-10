<template>
<!--    <div class="container-fluid">-->
<!--        <div class="row">-->
<!--            <div class="col">-->
<!--                -->
<!--            </div>-->
<!--        </div>-->
<!--    </div>-->
    <div class="card mt-4" style="width: 100%; padding: 10px;" v-if="!isCanceling">
        <h5>Contact Edit Form</h5>
        <div class="card-body">
            <div class="mt-2">
                <div style="display: inline-block; width: 10%">Name: </div>
                <div style="display: inline-block"><input type="text" v-model=contact.name></div>
            </div>
            <div class="mt-2">
                <div style="display: inline-block; width: 10%">Phone: </div>
                <div style="display: inline-block"><input type="text" v-model=contact.phone></div>
            </div>
            <div class="mt-2">
                <div style="display: inline-block; width: 10%">Email: </div>
                <div style="display: inline-block"><input type="text" v-model=contact.email></div>
            </div>

            <div class="mt-4">
                <button class="btn btn-primary active" @click="toggleIsSaving()" :disabled="isSaving || isCanceling">{{ saveBtnText }}</button>
                <button class="btn btn-danger active" @click="toggleIsCanceling()" :disabled="isSaving || isCanceling">{{ cancelBtnText }}</button>
            </div>
        </div>
    </div>
    <div v-else>
        <contact-list :contact=contact :is-expanded-prop=true></contact-list>
    </div>
</template>

<script>
export default {
    name: "ContactForm",

    data() {
        return {
            'isSaving': false,
            'isCanceling': false,
            'saveBtnText': 'Save',
            'cancelBtnText': 'Cancel'
        }
    },

    props: ["contact"],

    methods: {
        toggleIsSaving() {
            this.isSaving = !this.isSaving;
            this.saveBtnText = "Saving";
        },

        toggleIsCanceling() {
            this.isCanceling = !this.isCanceling;
            this.cancelBtnText = "Canceling";
        }
    },
}
</script>
