<script setup>
import GuestLayout from "@/Layouts/GuestLayout.vue";
import InputError from "@/Components/InputError.vue";
import InputLabel from "@/Components/InputLabel.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import TextInput from "@/Components/TextInput.vue";
import { Head, Link, useForm } from "@inertiajs/vue3";

const form = useForm({
    name: "",
    email: "",
    password: "",
    password_confirmation: "",
});

const submit = () => {
    form.post(route("register"), {
        onFinish: () => form.reset("password", "password_confirmation"),
    });
};
</script>

<template>
    <GuestLayout :show-breadcrumbs="false" :show-center="true">
        <Head title="Register" />

        <v-card
            variant="flat"
            class="p-4 mx-auto"
            border="dashed md"
            rounded="lg"
            min-width="360"
            max-width="480"
        >
            <v-card-title> Crear cuenta </v-card-title>
            <v-card-text>
                <form @submit.prevent="submit">
                    <v-container>
                        <v-row no-gutters>
                            <v-col cols="12">
                                <!-- Campo nombre -->
                                <v-text-field
                                    v-model="form.name"
                                    label="Nombre"
                                    :error-messages="form.errors.name"
                                />
                            </v-col>
                        </v-row>

                        <v-row no-gutters>
                            <v-col cols="12">
                                <!-- Campo Correo electrónico -->
                                <v-text-field
                                    v-model="form.email"
                                    label="Correo electrónico"
                                    :error-messages="form.errors.email"
                                />
                            </v-col>
                        </v-row>

                        <v-row no-gutters>
                            <v-col cols="12">
                                <!-- Campo Contraseña -->
                                <v-text-field
                                    v-model="form.password"
                                    label="Contraseña"
                                    :error-messages="form.errors.password"
                                />
                            </v-col>
                        </v-row>

                        <v-row no-gutters>
                            <v-col cols="12">
                                <!-- Campo Confirmar contraseña -->
                                <v-text-field
                                    v-model="form.password_confirmation"
                                    label="Confirmar contraseña"
                                    :error-messages="
                                        form.errors.password_confirmation
                                    "
                                />
                            </v-col>
                        </v-row>

                        <v-spacer></v-spacer>

                        <!-- Acciones -->
                        <v-row justify="end">
                            <Link :href="route('login')">
                                <v-btn variant="plain"
                                    >¿Ya tienes una cuenta? Inicia sesión</v-btn
                                >
                            </Link>
                            <v-btn type="submit" color="teal"
                                >Registrarme</v-btn
                            >
                        </v-row>
                    </v-container>
                </form>
            </v-card-text>
        </v-card>
    </GuestLayout>
</template>
