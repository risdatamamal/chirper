<script setup>
import Checkbox from "@/Components/Checkbox.vue";
import GuestLayout from "@/Layouts/GuestLayout.vue";
import AuthLayout from "@/Layouts/AuthLayout.vue";
import InputError from "@/Components/InputError.vue";
import InputLabel from "@/Components/InputLabel.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import TextInput from "@/Components/TextInput.vue";
import { Head, Link, useForm } from "@inertiajs/inertia-vue3";

const form = useForm({
    name: "",
    email: "",
    password: "",
    password_confirmation: "",
    terms: false,
});

const submit = () => {
    form.post(route("register"), {
        onFinish: () => form.reset("password", "password_confirmation"),
    });
};
</script>

<template>
    <AuthLayout>
        <Head title="Sign Up" />

        <form @submit.prevent="submit">
            <div class="h-screen flex justify-center items-center">
                <div
                    class="hidden md:block lg:w-1/3 bg-white h-full auth-background rounded-tr-lg rounded-br-lg"
                ></div>
                <div
                    class="w-auto md:w-2/4 lg:w-2/3 flex justify-center items-center"
                >
                    <div class="w-full lg:w-1/2 px-10 lg:px-0">
                        <h2 class="font-normal mb-6 text-3xl text-white">
                            Sign Up Account
                        </h2>
                        <div class="mb-6">
                            <div class="mb-4">
                                <InputLabel for="name" value="Full Name" />
                                <TextInput
                                    id="name"
                                    type="text"
                                    class="mt-1 block w-full"
                                    v-model="form.name"
                                    required
                                    placeholder="Write Your Name Here"
                                    autocomplete="name"
                                />
                                <InputError
                                    class="mt-2"
                                    :message="form.errors.name"
                                />
                            </div>
                        </div>
                        <div class="mb-6">
                            <div class="mb-4">
                                <InputLabel
                                    for="phone_number"
                                    value="Phone Number"
                                />
                                <TextInput
                                    id="phone_number"
                                    type="text"
                                    class="mt-1 block w-full"
                                    v-model="form.phone_number"
                                    required
                                    placeholder="Write your phone number here"
                                />
                                <InputError
                                    class="mt-2"
                                    :message="form.errors.phone_number"
                                />
                            </div>
                        </div>
                        <div class="mb-6">
                            <div class="mb-4">
                                <InputLabel for="email" value="Email Address" />
                                <TextInput
                                    id="email"
                                    type="email"
                                    class="mt-1 block w-full"
                                    v-model="form.email"
                                    required
                                    placeholder="Write your email address here"
                                />
                                <InputError
                                    class="mt-2"
                                    :message="form.errors.email"
                                />
                            </div>
                        </div>
                        <div class="mb-6">
                            <div class="mb-4">
                                <InputLabel for="password" value="Password" />
                                <TextInput
                                    id="password"
                                    type="password"
                                    class="mt-1 block w-full"
                                    v-model="form.password"
                                    required
                                    placeholder="Type your password here"
                                    autocomplete="new-password"
                                />
                                <InputError
                                    class="mt-2"
                                    :message="form.errors.password"
                                />
                            </div>
                        </div>
                        <div class="mb-6">
                            <div class="mb-4">
                                <InputLabel
                                    for="password_confirmation"
                                    value="Confirm Password"
                                />
                                <TextInput
                                    id="password_confirmation"
                                    type="password"
                                    class="mt-1 block w-full"
                                    v-model="form.password_confirmation"
                                    required
                                    placeholder="Type your confirmation password here"
                                    autocomplete="new-password"
                                />
                                <InputError
                                    class="mt-2"
                                    :message="form.errors.password_confirmation"
                                />
                            </div>
                        </div>
                        <div class="mb-6">
                            <div class="mb-4">
                                <label class="flex items-center">
                                    <Checkbox
                                        name="terms"
                                        v-model:checked="form.terms"
                                        required
                                    />
                                    <span class="ml-2 text-sm text-white"
                                        >Terms and Condition</span
                                    >
                                </label>
                            </div>
                        </div>
                        <div class="mb-6">
                            <div class="mb-4">
                                <PrimaryButton
                                    :class="{ 'opacity-25': form.processing }"
                                    :disabled="form.processing"
                                >
                                    Sign Up
                                </PrimaryButton>
                            </div>
                        </div>
                        <div class="mb-4 text-center">
                            <p class="text-white text-md">
                                Already have account?
                                <Link
                                    :href="route('login')"
                                    class="no-underline text-orange-button"
                                >
                                    Sign In
                                </Link>
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </form>
    </AuthLayout>
</template>

<style scoped>
.auth-background {
    background-image: url("assets/sign-up-background.jpg");
    background-position: center;
    background-size: cover;
}
</style>