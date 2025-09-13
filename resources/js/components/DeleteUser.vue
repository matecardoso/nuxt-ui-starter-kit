<script setup lang="ts">
import ProfileController from '@/actions/App/Http/Controllers/Settings/ProfileController';
import { Form } from '@inertiajs/vue3';
import { ref } from 'vue';

// Components
import HeadingSmall from '@/components/HeadingSmall.vue';
import InputError from '@/components/InputError.vue';

const passwordInput = ref<HTMLInputElement | null>(null);
const isModalOpen = ref(false);
</script>

<template>
    <div class="space-y-6">
        <HeadingSmall title="Delete account" description="Delete your account and all of its resources" />
        <div class="space-y-4 rounded-lg border border-red-100 bg-red-50 p-4 dark:border-red-200/10 dark:bg-red-700/10">
            <div class="relative space-y-0.5 text-red-600 dark:text-red-100">
                <p class="font-medium">Warning</p>
                <p class="text-sm">Please proceed with caution, this cannot be undone.</p>
            </div>

            <UButton color="red" data-test="delete-user-button" @click="isModalOpen = true">Delete account</UButton>

            <UModal v-model="isModalOpen">
                <div class="p-4">
                    <Form
                        v-bind="ProfileController.destroy.form()"
                        reset-on-success
                        @error="() => passwordInput?.focus()"
                        :options="{
                            preserveScroll: true,
                        }"
                        class="space-y-6"
                        v-slot="{ errors, processing, reset, clearErrors }"
                    >
                        <div class="space-y-3">
                            <h2 class="text-lg font-bold">Are you sure you want to delete your account?</h2>
                            <p class="text-sm text-gray-500">
                                Once your account is deleted, all of its resources and data will also be permanently deleted. Please enter your
                                password to confirm you would like to permanently delete your account.
                            </p>
                        </div>

                        <div class="grid gap-2">
                            <UInput
                                id="password"
                                type="password"
                                name="password"
                                ref="passwordInput"
                                placeholder="Password"
                                v-model="ProfileController.destroy.form().password"
                            />
                            <InputError :message="errors.password" />
                        </div>

                        <div class="flex justify-end gap-2">
                            <UButton
                                color="gray"
                                @click="
                                    () => {
                                        clearErrors();
                                        reset();
                                        isModalOpen = false;
                                    }
                                "
                            >
                                Cancel
                            </UButton>

                            <UButton type="submit" color="red" :disabled="processing" data-test="confirm-delete-user-button">
                                Delete account
                            </UButton>
                        </div>
                    </Form>
                </div>
            </UModal>
        </div>
    </div>
</template>
