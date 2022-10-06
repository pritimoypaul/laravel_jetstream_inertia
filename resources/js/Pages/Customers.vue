<script>
import AppLayout from "@/Layouts/AppLayout.vue";
import { Inertia } from "@inertiajs/inertia";
import { Link } from "@inertiajs/inertia-vue3";
import { TrashIcon, PencilAltIcon } from "@heroicons/vue/outline";

export default {
    components: {
        AppLayout,
        Link,
        TrashIcon,
        PencilAltIcon,
    },
    props: {
        customers: Object,
    },
    methods: {
        deleteCustomer(id) {
            axios
                .delete("/customers/delete/" + id)
                .then((res) => {
                    console.log(res);
                    this.$toast.success("Successfully Deleted.");
                    Inertia.reload();
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
                Customers Dashboard
            </h2>
        </template>

        <div class="max-w-7xl mx-auto py-4 px-8">
            <Link
                class="float-right bg-indigo-500 px-4 py-2 rounded-sm text-lg font-semibold text-white"
                href="/customers/create"
                >Add Customer</Link
            >
        </div>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div
                    class="bg-white overflow-hidden shadow-xl sm:rounded-lg p-6"
                >
                    <div class="text-lg">Customers Page</div>
                    <br />
                    <div>Find detailed information about your clients</div>
                    <br />

                    <div class="overflow-x-auto relative">
                        <table
                            class="w-full text-sm text-left text-gray-500 dark:text-gray-400"
                        >
                            <thead
                                class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400"
                            >
                                <tr>
                                    <th scope="col" class="py-3 px-6">
                                        Customer name
                                    </th>
                                    <th scope="col" class="py-3 px-6">Email</th>
                                    <th scope="col" class="py-3 px-6">
                                        Phone Number
                                    </th>
                                    <th scope="col" class="py-3 px-6">
                                        Last Bill
                                    </th>
                                    <th scope="col" class="py-3 px-4">
                                        Actions
                                    </th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr
                                    v-for="customer in customers"
                                    :key="customer.id"
                                    class="bg-white border-b dark:bg-gray-800 dark:border-gray-700"
                                >
                                    <th
                                        scope="row"
                                        class="py-4 px-6 font-medium text-gray-900 whitespace-nowrap dark:text-white"
                                    >
                                        {{ customer.name }}
                                    </th>
                                    <td class="py-4 px-6">
                                        {{ customer.email }}
                                    </td>
                                    <td class="py-4 px-6">
                                        {{ customer.phone_num }}
                                    </td>
                                    <td class="py-4 px-6">
                                        ${{ customer.bill }}
                                    </td>
                                    <td class="py-4 px-6 flex">
                                        <PencilAltIcon
                                            class="h-5 w-5 text-blue-500 cursor-pointer"
                                        />
                                        &nbsp;
                                        <TrashIcon
                                            @click="deleteCustomer(customer.id)"
                                            class="h-5 w-5 text-red-500 cursor-pointer"
                                        />
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
