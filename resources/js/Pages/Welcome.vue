<script setup>
import { ref, computed, defineProps } from "vue";
import { Head, Link, useForm, usePage } from "@inertiajs/vue3";
import ApplicationLogo from "@/Components/ApplicationLogo.vue";

defineProps({
    canLogin: {
        type: Boolean,
    },
    canRegister: {
        type: Boolean,
    },
    laravelVersion: {
        type: String,
        required: true,
    },
    phpVersion: {
        type: String,
        required: true,
    },
});

const appName = usePage().props.app.name;
</script>

<template>
    <Head title="Home" />
    <v-app>
        <v-layout class="rounded rounded-md border">
            <v-app-bar>
                <template v-slot:prepend>
                    <!-- Logo -->
                    <div class="shrink-0 flex items-center">
                        <Link :href="'/'">
                            <ApplicationLogo
                                class="block h-9 w-auto fill-current text-gray-800"
                            />
                        </Link>
                    </div>
                </template>
                <Link :href="'/'" class="ml-5">
                    <v-app-bar-title>{{ appName }}</v-app-bar-title>
                </Link>
                <v-spacer></v-spacer>
                <Link :href="route('login')" method="get">
                    <v-btn text>Iniciar sesión</v-btn>
                </Link>
                <Link :href="route('register')" method="get">
                    <v-btn text>Crear cuenta</v-btn>
                </Link>
            </v-app-bar>

            <v-navigation-drawer>
                <v-list nav>
                    <v-list-item title="Drawer left" link></v-list-item>
                </v-list>
            </v-navigation-drawer>

            <v-navigation-drawer location="right">
                <v-list nav>
                    <v-list-item title="Drawer right" link></v-list-item>
                </v-list>
            </v-navigation-drawer>

            <v-main>
                <v-container fluid>
                    <v-sheet
                        border="dashed md"
                        color="surface-light"
                        height="200"
                        rounded="lg"
                        width="100%"
                    ></v-sheet>
                </v-container>
            </v-main>
        </v-layout>
    </v-app>
</template>

<style>
.bg-dots-darker {
    background-image: url("data:image/svg+xml,%3Csvg width='30' height='30' viewBox='0 0 30 30' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M1.22676 0C1.91374 0 2.45351 0.539773 2.45351 1.22676C2.45351 1.91374 1.91374 2.45351 1.22676 2.45351C0.539773 2.45351 0 1.91374 0 1.22676C0 0.539773 0.539773 0 1.22676 0Z' fill='rgba(0,0,0,0.07)'/%3E%3C/svg%3E");
}
@media (prefers-color-scheme: dark) {
    .dark\:bg-dots-lighter {
        background-image: url("data:image/svg+xml,%3Csvg width='30' height='30' viewBox='0 0 30 30' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M1.22676 0C1.91374 0 2.45351 0.539773 2.45351 1.22676C2.45351 1.91374 1.91374 2.45351 1.22676 2.45351C0.539773 2.45351 0 1.91374 0 1.22676C0 0.539773 0.539773 0 1.22676 0Z' fill='rgba(255,255,255,0.07)'/%3E%3C/svg%3E");
    }
}
</style>
