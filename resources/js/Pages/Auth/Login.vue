<script setup>
import Checkbox from "@/Components/Checkbox.vue";
import GuestLayout from "@/Layouts/GuestLayout.vue";
import AuthLayout from "@/Layouts/AuthLayout.vue";
import InputError from "@/Components/InputError.vue";
import InputLabel from "@/Components/InputLabel.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import TextInput from "@/Components/TextInput.vue";
import { Head, Link, useForm } from "@inertiajs/inertia-vue3";

defineProps({
    canResetPassword: Boolean,
    status: String,
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
</script>

<template>
    <AuthLayout>
        <Head title="Sign In" />

        <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
            {{ status }}
        </div>

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
                            Sign In to Your Account
                        </h2>
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
                                    autocomplete="username"
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
                                    placeholder="Write your password here"
                                    autocomplete="current-password"
                                />
                                <InputError
                                    class="mt-2"
                                    :message="form.errors.password"
                                />
                            </div>
                        </div>
                        <div class="mb-6">
                            <div class="mb-4">
                                <label class="flex items-center">
                                    <Checkbox
                                        name="remember"
                                        v-model:checked="form.remember"
                                    />
                                    <span class="ml-2 text-sm text-white"
                                        >Remember me</span
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
                                    Sign In
                                </PrimaryButton>
                            </div>
                        </div>
                        <div class="text-center">
                            <p class="text-white text-md">
                                Don't have account?
                                <Link
                                    :href="route('register')"
                                    class="no-underline text-orange-button"
                                >
                                    Sign Up
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
    background-image: url("assets/sign-in-background.jpg");
    background-position: center;
    background-size: cover;
}
</style>