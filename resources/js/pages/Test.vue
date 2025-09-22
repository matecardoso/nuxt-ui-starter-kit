<script setup lang="ts">
import { Head } from '@inertiajs/vue3';
</script>

<template>
    <Head title="Test Nuxt UI Components" />
    
    <UApp>
        <div class="min-h-screen bg-gray-50 p-8">
            <div class="max-w-4xl mx-auto space-y-8">
                <div>
                    <h1 class="text-3xl font-bold text-gray-900 mb-2">
                        Nuxt UI 4 Test Page
                    </h1>
                    <p class="text-gray-600">
                        Testing Nuxt UI components in Laravel + Inertia + Vue setup
                    </p>
                </div>

                <!-- Button Tests -->
                <UCard>
                    <template #header>
                        <h2 class="text-xl font-semibold">Button Components</h2>
                    </template>
                    
                    <div class="space-y-4">
                        <div class="flex gap-4 flex-wrap">
                            <UButton color="primary" variant="solid">Primary Button</UButton>
                            <UButton color="secondary" variant="outline">Secondary Button</UButton>
                            <UButton color="success" variant="soft">Success Button</UButton>
                            <UButton color="warning" variant="ghost">Warning Button</UButton>
                            <UButton color="error" variant="link">Error Button</UButton>
                        </div>
                        
                        <div class="flex gap-4 flex-wrap">
                            <UButton size="xs">Extra Small</UButton>
                            <UButton size="sm">Small</UButton>
                            <UButton size="md">Medium</UButton>
                            <UButton size="lg">Large</UButton>
                            <UButton size="xl">Extra Large</UButton>
                        </div>

                        <div class="flex gap-4 flex-wrap">
                            <UButton icon="i-heroicons-plus" loading>Loading</UButton>
                            <UButton disabled>Disabled</UButton>
                            <UButton trailing-icon="i-heroicons-arrow-right">With Icon</UButton>
                        </div>
                    </div>
                </UCard>

                <!-- Badge Tests -->
                <UCard>
                    <template #header>
                        <h2 class="text-xl font-semibold">Badge Components</h2>
                    </template>
                    
                    <div class="space-y-4">
                        <div class="flex gap-4 flex-wrap">
                            <UBadge color="primary">Primary</UBadge>
                            <UBadge color="secondary">Secondary</UBadge>
                            <UBadge color="success">Success</UBadge>
                            <UBadge color="warning">Warning</UBadge>
                            <UBadge color="error">Error</UBadge>
                        </div>
                        
                        <div class="flex gap-4 flex-wrap">
                            <UBadge variant="solid">Solid</UBadge>
                            <UBadge variant="outline">Outline</UBadge>
                            <UBadge variant="soft">Soft</UBadge>
                            <UBadge variant="subtle">Subtle</UBadge>
                        </div>
                    </div>
                </UCard>

                <!-- Alert Tests -->
                <UCard>
                    <template #header>
                        <h2 class="text-xl font-semibold">Alert Components</h2>
                    </template>
                    
                    <div class="space-y-4">
                        <UAlert
                            icon="i-heroicons-information-circle"
                            color="primary"
                            title="Information"
                            description="This is an informational alert message."
                        />
                        
                        <UAlert
                            icon="i-heroicons-check-circle"
                            color="success"
                            title="Success"
                            description="Operation completed successfully!"
                        />
                        
                        <UAlert
                            icon="i-heroicons-exclamation-triangle"
                            color="warning"
                            title="Warning"
                            description="Please review this warning message."
                        />
                        
                        <UAlert
                            icon="i-heroicons-x-circle"
                            color="error"
                            title="Error"
                            description="An error has occurred. Please try again."
                        />
                    </div>
                </UCard>

                <!-- Input Tests -->
                <UCard>
                    <template #header>
                        <h2 class="text-xl font-semibold">Input Components</h2>
                    </template>
                    
                    <div class="space-y-4">
                        <UInput placeholder="Enter your name" />
                        <UInput placeholder="Disabled input" disabled />
                        <UInput placeholder="Input with icon" icon="i-heroicons-user" />
                        <UInput placeholder="Input with trailing icon" trailing-icon="i-heroicons-magnifying-glass" />
                        <UTextarea placeholder="Enter your message..." />
                    </div>
                </UCard>

                <!-- Avatar Tests -->
                <UCard>
                    <template #header>
                        <h2 class="text-xl font-semibold">Avatar Components</h2>
                    </template>
                    
                    <div class="space-y-4">
                        <div class="flex gap-4 items-center">
                            <UAvatar src="https://github.com/octocat.png" alt="GitHub" />
                            <UAvatar text="JD" />
                            <UAvatar icon="i-heroicons-user" />
                            <UAvatar size="xs" text="XS" />
                            <UAvatar size="sm" text="SM" />
                            <UAvatar size="md" text="MD" />
                            <UAvatar size="lg" text="LG" />
                            <UAvatar size="xl" text="XL" />
                        </div>
                    </div>
                </UCard>
            </div>
        </div>
    </UApp>
</template>