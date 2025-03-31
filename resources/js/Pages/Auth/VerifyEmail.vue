<script setup>
import { computed } from "vue";
import GuestLayout from "@/Layouts/GuestLayout.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import { Head, Link, useForm } from "@inertiajs/vue3";

const props = defineProps({
    status: {
        type: String,
    },
});

const form = useForm({});

const submit = () => {
    form.post(route("verification.send"));
};

const verificationLinkSent = computed(
    () => props.status === "verification-link-sent"
);
</script>

<template>
    <GuestLayout :show-breadcrumbs="false" :show-center="true" :show-app-bar="false">
        <Head title="Verificar cuenta" />

        <v-card
            variant="flat"
            class="p-4 mx-auto"
            border="dashed md"
            rounded="lg"
            min-width="360"
            max-width="480"
        >
            <v-card-title primary-title> Verificar cuenta </v-card-title>
            <v-card-text>
                <v-row no-gutters>
                    <v-col cols="12">
                        ¡Gracias por registrarte! Antes de comenzar, ¿podrías verificar tu dirección de correo electrónico haciendo clic en el enlace que te acabamos de enviar? Si no recibiste el correo, con gusto te enviaremos otro.
                    </v-col>
                </v-row>
                <v-row v-if="verificationLinkSent" no-gutters class="m-2">
                    <v-alert closable type="success" variant="tonal">
                        <v-alert-text>
                            Se ha enviado un nuevo enlace de verificación a la dirección de correo electrónico que proporcionaste durante el registro.
                        </v-alert-text>
                    </v-alert>
                </v-row>
                <form @submit.prevent="submit">
                    <v-container class="mt-2">
                        <v-row justify="end">
                            <v-btn type="submit" color="teal" class="me-2">
                                Verificar mi cuenta
                            </v-btn>
                            <Link :href="route('logout')" method="post">
                                <v-btn color="red" class="me-2">
                                    Cerrar sesión
                                </v-btn>
                            </Link>
                        </v-row>
                    </v-container>
                </form>
            </v-card-text>
        </v-card>
    </GuestLayout>
</template>
