<script setup>
import { ref, computed, defineProps } from "vue";
import GuestLayout from "@/Layouts/GuestLayout.vue";
import { Head, Link, useForm } from "@inertiajs/vue3";

defineProps({
    canResetPassword: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});

const form = useForm({
    email: "",
    password: "",
    remember: false,
});

const submit = () => {
    form.post(route("login"), {
        onFinish: () => form.reset("password"),
    });
};

// Función para limpiar los campos
const clear = () => {
    form.email = "";
    form.password = "";
    form.remember = false;
};
</script>

<template>
    <GuestLayout :show-breadcrumbs="false" :show-center="true">
        <Head title="Iniciar sesión" />

        <v-card
            variant="flat"
            class="p-4 mx-auto"
            border="dashed md"
            rounded="lg"
            min-width="360"
            max-width="480"
        >
            <v-card-title>Iniciar sesión</v-card-title>
            <v-card-text>
                <v-row v-if="status" no-gutters class="mb-2">
                    <v-alert closable :text="status" type="success" variant="tonal"></v-alert>
                </v-row>
                <form @submit.prevent="submit">
                    <v-container>
                        <v-row no-gutters>
                            <v-col cols="12">
                                <!-- Campo Nombre -->
                                <v-text-field
                                    v-model="form.email"
                                    :counter="10"
                                    label="Correo electrónico"
                                    :error-messages="form.errors.email"
                                ></v-text-field>
                            </v-col>
                        </v-row>

                        <v-row no-gutters >
                            <v-col cols="12">
                                <!-- Campo Correo Electrónico -->
                                <v-text-field
                                    v-model="form.password"
                                    label="Contraseña"
                                    :error-messages="form.errors.password"
                                ></v-text-field>
                            </v-col>
                        </v-row>

                        <v-row no-gutters>
                            <v-col cols="12">
                                <!-- Campo Checkbox -->
                                <v-checkbox
                                    v-model="form.remember"
                                    label="Recuérdeme"
                                ></v-checkbox>
                            </v-col>
                        </v-row>

                        <v-row no-gutters> 
                            <v-row justify="end">
                                <!-- Acciones -->
                                <Link :href="route('password.request')">
                                    <v-btn variant="plain">
                                        ¿Olvidaste tu contraseña?
                                    </v-btn>
                                </Link>
                                <!-- Botón de Limpiar -->
                                <v-btn type="submit" class="me-4" color="teal"
                                    >Entrar</v-btn
                                >
                            </v-row>
                        </v-row>
                    </v-container>
                </form>
            </v-card-text>
        </v-card>
    </GuestLayout>
</template>
