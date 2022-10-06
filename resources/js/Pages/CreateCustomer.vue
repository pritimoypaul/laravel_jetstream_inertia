<script>
import AppLayout from "@/Layouts/AppLayout.vue";
import { Link } from "@inertiajs/inertia-vue3";
import axios from "axios";

export default {
    components: {
        AppLayout,
        Link,
    },
    props: {
        customers: Object,
    },
    data: function () {
        return {
            name: "",
            email: "",
            phone_num: "",
            bill: "",
        };
    },
    methods: {
        createCustomer() {
            axios
                .post("/customers/store", {
                    name: this.name,
                    email: this.email,
                    phone_num: this.phone_num,
                    bill: this.bill,
                })
                .then((response) => {
                    (this.name = ""),
                        (this.email = ""),
                        (this.phone_num = ""),
                        (this.bill = "");
                    this.$toast.success("New Customer Added!");
                })
                .catch((err) => {
                    console.log(err);
                    this.$toast.error("There was an error!");
                });
        },
    },
};
</script>

<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Add New Customer
            </h2>
        </template>

        <div class="">
            <!-- form -->

            <div class="max-w-6xl mx-auto py-12">
                <div class="mt-10 sm:mt-0">
                    <div class="md:grid md:grid-cols-3 md:gap-6">
                        <div class="md:col-span-1">
                            <div class="px-4 sm:px-0">
                                <h3
                                    class="text-lg font-medium leading-6 text-gray-900"
                                >
                                    Personal Information
                                </h3>
                                <p class="mt-1 text-sm text-gray-600">
                                    Use a permanent address where you can
                                    receive mail.
                                </p>
                            </div>
                        </div>
                        <div class="mt-5 md:mt-0 md:col-span-2">
                            <div class="shadow overflow-hidden sm:rounded-md">
                                <div class="px-4 py-5 bg-white sm:p-6">
                                    <div class="grid grid-cols-6 gap-6">
                                        <div class="col-span-6">
                                            <label
                                                for="name"
                                                class="block text-sm font-medium text-gray-700"
                                                >Customers name</label
                                            >
                                            <input
                                                type="text"
                                                name="name"
                                                v-model="name"
                                                id="name"
                                                class="mt-1 focus:ring-indigo-500 focus:border-indigo-500 block w-full shadow-sm sm:text-sm border-gray-300 rounded-md"
                                            />
                                        </div>

                                        <div class="col-span-6">
                                            <label
                                                for="email-address"
                                                class="block text-sm font-medium text-gray-700"
                                                >Email address</label
                                            >
                                            <input
                                                type="text"
                                                name="email-address"
                                                v-model="email"
                                                id="email-address"
                                                class="mt-1 focus:ring-indigo-500 focus:border-indigo-500 block w-full shadow-sm sm:text-sm border-gray-300 rounded-md"
                                            />
                                        </div>

                                        <div class="col-span-6">
                                            <label
                                                for="phone_num"
                                                class="block text-sm font-medium text-gray-700"
                                                >Phone Number</label
                                            >
                                            <input
                                                type="text"
                                                name="phone_num"
                                                v-model="phone_num"
                                                id="phone_num"
                                                class="mt-1 focus:ring-indigo-500 focus:border-indigo-500 block w-full shadow-sm sm:text-sm border-gray-300 rounded-md"
                                            />
                                        </div>

                                        <div
                                            class="col-span-6 sm:col-span-6 lg:col-span-2"
                                        >
                                            <label
                                                for="bill"
                                                class="block text-sm font-medium text-gray-700"
                                                >Last Bill</label
                                            >
                                            <input
                                                type="text"
                                                name="bill"
                                                v-model="bill"
                                                id="bill"
                                                class="mt-1 focus:ring-indigo-500 focus:border-indigo-500 block w-full shadow-sm sm:text-sm border-gray-300 rounded-md"
                                            />
                                        </div>
                                    </div>
                                </div>
                                <div
                                    class="px-4 py-3 bg-gray-50 text-right sm:px-6"
                                >
                                    <button
                                        @click.prevent="createCustomer"
                                        class="inline-flex justify-center py-2 px-4 border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
                                    >
                                        Save
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
