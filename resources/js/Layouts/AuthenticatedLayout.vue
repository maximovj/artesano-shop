<script setup>
import { ref, computed, defineProps } from 'vue';
import ApplicationLogo from '@/Components/ApplicationLogo.vue';
import { Link } from '@inertiajs/vue3';

const items = ref([]);

items.value = window.location.pathname
  .split("/")
  .filter(Boolean)
  .map((el, index, arr) => ({
    title: el,
    disabled: index === arr.length - 1, // El último breadcrumb está deshabilitado
    href: "/" + arr.slice(0, index + 1).join("/")
  }));
</script>

<template>
    <v-app>
        <v-layout class="rounded rounded-md border">
            <!-- Page Heading -->
            <v-app-bar :elevation="2" rounded>
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
                    <v-app-bar-title> ArtesanoShop </v-app-bar-title>
                </Link>

                <v-spacer></v-spacer>

                <v-menu>
                    <template v-slot:activator="{ props }">
                        <v-btn icon="mdi-dots-vertical" variant="plain" v-bind="props"></v-btn>
                    </template>

                    <v-list density="compact" class="pa-2">
                        <v-list-subheader>Menú</v-list-subheader>

                        <!-- Grupo de items de menú -->
                        <v-list-item-group color="primary">

                            <!-- Dashboard -->
                            <Link :href="route('dashboard')" :active="route().current('dashboard')">
                            <v-list-item>
                                <template v-slot:prepend>
                                    <v-icon left>mdi-home</v-icon>
                                </template>
                                <v-list-item-title>
                                    Dashboard
                                </v-list-item-title>
                            </v-list-item>
                            </Link>

                            <!-- Profile -->
                            <Link href="/profile">
                            <v-list-item>
                                <template v-slot:prepend>
                                    <v-icon left>mdi-account</v-icon>
                                </template>
                                <v-list-item-title>
                                    Profile
                                </v-list-item-title>
                            </v-list-item>
                            </Link>

                            <!-- Agregar separadores opcionales -->
                            <v-divider></v-divider>

                            <!-- Agregar más ítems -->
                            <Link :href="route('logout')" method="post">
                                <v-list-item>
                                    <template v-slot:prepend>
                                        <v-icon left>mdi-exit-to-app</v-icon>
                                    </template>
                                    <v-list-item-title>
                                        Salir
                                    </v-list-item-title>
                                </v-list-item>
                            </Link>
                        </v-list-item-group>
                    </v-list>
                </v-menu>
            </v-app-bar>
            <!-- <v-navigation-drawer expand-on-hover permanent rail>
                <v-list>
                    <v-list-item prepend-avatar="https://randomuser.me/api/portraits/women/85.jpg"
                        subtitle="sandra_a88@gmailcom" title="Sandra Adams"></v-list-item>
                </v-list>

                <v-divider></v-divider>

                <v-list density="compact" nav>
                    <v-list-item prepend-icon="mdi-folder" title="My Files" value="myfiles"></v-list-item>
                    <v-list-item prepend-icon="mdi-account-multiple" title="Shared with me"
                        value="shared"></v-list-item>
                    <v-list-item prepend-icon="mdi-star" title="Starred" value="starred"></v-list-item>
                </v-list>
            </v-navigation-drawer> -->
            <v-main >
                <v-container fluid>
                    <v-breadcrumbs :items="items">
                        <template v-slot:prepend>
                        <v-icon icon="$vuetify" size="small"></v-icon>
                        </template>
                    </v-breadcrumbs>
                    <slot />
                </v-container>
            </v-main>
        </v-layout>
    </v-app>
</template>

<style scoped></style>
