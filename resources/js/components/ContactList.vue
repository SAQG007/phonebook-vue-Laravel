<template>
<!--    <div class="container-fluid">-->
<!--        <div class="row">-->
<!--            <div class="col">-->
<!--                -->
<!--            </div>-->
<!--        </div>-->
<!--    </div>-->

    <div class="card mt-4 mb-4" style="width: 100%; padding: 10px;" @click="toggleIsExpanded()" v-if="!isEditing">
        <h5 style="cursor: pointer">{{ contact.name }}</h5>

        <div class="card-body" v-if="isExpanded">

            <div class="mt-2">
                <div style="display: inline-block; width: 10%">ID: </div>
                <div style="display: inline-block">{{ contact.id }}</div>
            </div>
            <div class="mt-2">
                <div style="display: inline-block; width: 10%">Phone: </div>
                <div style="display: inline-block">{{ contact.phone }}</div>
            </div>
            <div class="mt-2">
                <div style="display: inline-block; width: 10%">Email: </div>
                <div style="display: inline-block">{{ contact.email }}</div>
            </div>

            <div class="mt-4">
                <button class="btn btn-warning active" @click="toggleIsEditing()">Edit</button>
                <button class="btn btn-danger active" @click="$emit('deleteContact', contact.id)">Delete</button>
                <button class="btn btn-warning" @click="$emit('edit', contact.name)">Emit</button>
            </div>
        </div>
    </div>
    <div v-else>
        <contact-form :contact=contactCopy></contact-form>
    </div>
</template>

<script>
export default {
    name: "ContactList",

    data() {
        return {
            isExpanded: this.isExpandedProp,
            isEditing: false,
            contactCopy: this.contact,
        }
    },

    props: {
        contact: {
            require: true,
        },

        isExpandedProp: {
            default: false,
        },
    },

    methods: {
        toggleIsExpanded() {
            this.isExpanded = !this.isExpanded;
        }, // toggleIsExpanded()

        toggleIsEditing() {
            this.isEditing = !this.isEditing;
        }, // toggleIsEditing()
    },
}
</script>
