<script setup>
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import Message from "@/Components/Message.vue";
import InputError from "@/Components/InputError.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import { useForm, Head } from "@inertiajs/vue3";

defineProps(["messages"]);

const form = useForm({
    message: "",
});
</script>

<template>
    <Head title="Messages" />

    <AuthenticatedLayout>
        <div class="max-w-2xl mx-auto p-4 sm:p-6 lg:p-8">
            <form
                @submit.prevent="
                    form.post(route('messages.store'), {
                        onSuccess: () => form.reset(),
                    })
                "
            >
                <textarea
                    v-model="form.message"
                    placeholder="Your message here..."
                    class="block w-full border-gray-500 focus:border-blue-600 focus:ring focus:ring-blue-600 focus:ring-opacity-50 rounded-md shadow-sm"
                ></textarea>
                <InputError :message="form.errors.message" class="mt-2" />
                <PrimaryButton class="mt-4">Post!</PrimaryButton>
            </form>
            <div class="mt-6 bg-white shadow-sm rounded-lg divide-y">
                <Message
                    v-for="message in messages"
                    :key="message.id"
                    :message="message"
                />
            </div>
        </div>
    </AuthenticatedLayout>
</template>
