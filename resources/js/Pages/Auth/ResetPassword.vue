<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, useForm } from '@inertiajs/vue3';

const props = defineProps({
    email: {
        type: String,
        required: true,
    },
    token: {
        type: String,
        required: true,
    },
});

const form = useForm({
    token: props.token,
    email: props.email,
    password: '',
    password_confirmation: '',
});

const submit = () => {
    form.post(route('password.store'), {
        onFinish: () => form.reset('password', 'password_confirmation'),
    });
};
</script>

<template>
    <GuestLayout :show-breadcrumbs="false" :show-center="true">
        <Head title="Restablecer contraseña" />

        <v-card
            variant="flat"
            class="p-4 mx-auto"
            border="dashed md"
            rounded="lg"
            min-width="360"
            max-width="480"
        >
            <v-card-title>Restablecer contraseña</v-card-title>
            <v-card-text>
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

                        <v-row no-gutters>
                            <v-col cols="12">
                                <!-- Campo Contraseña -->
                                <v-text-field
                                    v-model="form.password"
                                    label="Contraseña"
                                    :error-messages="form.errors.password"
                                ></v-text-field>
                            </v-col>
                        </v-row>

                        <v-row no-gutters>
                            <v-col cols="12">
                                <!-- Campo Confirmar contraseña -->
                                <v-text-field
                                    v-model="form.password_confirmation"
                                    label="Confirmar contraseña"
                                    :error-messages="form.errors.password_confirmation"
                                ></v-text-field>
                            </v-col>
                        </v-row>
                        
                        <v-row no-gutters> 
                            <v-row justify="end">
                                <!-- Botón de Limpiar -->
                                <v-btn type="submit" class="me-4" color="teal"
                                    >Restablecer contraseña</v-btn
                                >
                            </v-row>
                        </v-row>
                    </v-container>
                </form>
            </v-card-text>
        </v-card>
    </GuestLayout>
</template>
