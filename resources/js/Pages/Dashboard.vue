<script setup lang="ts">
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
</script>
<template>
    <Head title="Dashboard" />
    <AuthenticatedLayout>
        <template v-slot:content>
            <div class="bg-white overflow-hidden ">
                <div class="p-6 text-gray-900">You're logged in!</div>
            </div>
        </template>
    </AuthenticatedLayout>
</template>
