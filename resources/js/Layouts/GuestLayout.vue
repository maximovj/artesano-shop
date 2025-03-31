<script setup>
import { ref, computed, defineProps } from 'vue';
import ApplicationLogo from '@/Components/ApplicationLogo.vue';
import { Link, usePage } from "@inertiajs/vue3";

const props = defineProps({
    showBreadcrumbs: {
        type: Boolean,
        default: true,
    },
    showCenter: {
        type: Boolean,
        default: false,
    },
    showAppBar: {
        type: Boolean,
        default: true,
    }
});

const appName = usePage().props.app.name;

const items = ref([]);
items.value = window.location.pathname
  .split("/")
  .filter(Boolean)
  .map((el, index, arr) => ({
    title: el,
    disabled: index === arr.length - 1, // El último breadcrumb está deshabilitado
    href: "/" + arr.slice(0, index + 1).join("/")
}));

const centeredStyle = computed(() => ({
  'min-height': props.showCenter ? '100vh' : 'auto', // Estilo dinámico
}));

</script>

<template>
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
                <div v-show="showAppBar">

                    <Link :href="route('login')" method="get">
                        <v-btn text>Iniciar sesión</v-btn>
                    </Link>
                    <Link :href="route('register')" method="get">
                        <v-btn text>Crear cuenta</v-btn>
                    </Link>
                </div>
            </v-app-bar>

            <v-main class="" height="300">
                <v-container :class="{'d-flex justify-center align-center': showCenter}" :style="centeredStyle">
                    <v-breadcrumbs v-show="showBreadcrumbs" :items="items">
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
