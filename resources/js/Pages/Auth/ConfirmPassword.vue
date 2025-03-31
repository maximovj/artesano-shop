<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, useForm } from '@inertiajs/vue3';

const form = useForm({
    password: '',
});

const submit = () => {
    form.post(route('password.confirm'), {
        onFinish: () => form.reset(),
    });
};
</script>

<template>
    <GuestLayout :show-app-bar="false" :show-breadcrumbs="false" :show-center="true">
        <Head title="Confirm Password" />

        <v-card>
            <v-card-title primary-title>
                Confirmar contraseña
            </v-card-title>
            <v-card-text>
                <v-row no-gutters>
                    <div>
                        Esta es un área segura de la aplicación. Por favor, confirma tu contraseña antes de continuar
                    </div>
                </v-row>
                <form @submit.prevent="submit">
                    <v-container>
                        <!-- Campo Contraseña -->
                        <v-row no-gutters class="mb-2">
                            <v-col cols="12">
                                <v-text-field
                                    v-model="form.password"
                                    type="password"
                                    id="password"
                                    label="Contraseña"
                                    :error-messages="form.errors.password"
                                ></v-text-field>
                            </v-col>
                        </v-row>

                        <v-row no-gutters>
                            <v-col cols="12">
                                <v-btn 
                                    type="submit" 
                                    :active="form.processing"
                                    active-color="grey-darken-3" 
                                    color="teal">Confirmar</v-btn>
                            </v-col>
                        </v-row>
                    </v-container>
                </form>
            </v-card-text>
        </v-card>
    </GuestLayout>
</template>
