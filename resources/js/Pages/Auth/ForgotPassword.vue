<script setup>
import GuestLayout from "@/Layouts/GuestLayout.vue";
import InputError from "@/Components/InputError.vue";
import InputLabel from "@/Components/InputLabel.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import TextInput from "@/Components/TextInput.vue";
import { Head, useForm } from "@inertiajs/vue3";

defineProps({
    status: {
        type: String,
    },
});

const form = useForm({
    email: "",
});

const submit = () => {
    form.post(route("password.email"));
};
</script>

<template>
    <GuestLayout :show-breadcrumbs="false" :show-center="true">
        <Head title="Forgot Password" />

        

        <v-card variant="flat" class="p-4 mx-auto" border="dashed md" rounded="lg" min-width="360" max-width="480">
            <v-card-title primary-title> Recuperar contraseña </v-card-title>
            <v-card-text>
                <v-row v-if="status" no-gutters class="mb-2">
                    <v-alert closable :text="status" type="success" variant="tonal"></v-alert>
                </v-row>
                <v-row class="mb-2 mt-2" no-gutters>
                    <v-col cols="12">
                    ¿Olvidaste tu contraseña? No hay problema. Solo indícanos tu
                    dirección de correo electrónico y te enviaremos un enlace para
                    restablecer tu contraseña, que te permitirá elegir una nueva.
                    </v-col>
                </v-row>
                <form @submit.prevent="submit">
                    <v-container>
                        <v-row no-gutters>
                            <v-col cols="12">
                                <v-text-field
                                    v-model="form.email"
                                    label="Correo electrónico"
                                    :error-messages="form.errors.email"
                                />
                            </v-col>
                        </v-row>

                        <v-row no-gutters>
                            <v-col cols="12" class="text-right">
                                <v-btn type="submit" color="teal"
                                    >Recuperar cuenta</v-btn
                                >
                            </v-col>
                        </v-row>
                    </v-container>
                </form>
            </v-card-text>
        </v-card>
    </GuestLayout>
</template>
