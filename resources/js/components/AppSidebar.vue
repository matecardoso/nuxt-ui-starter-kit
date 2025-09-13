<script setup lang="ts">
import { getInitials } from '@/composables/useInitials';
import { dashboard, logout } from '@/routes';
import { edit } from '@/routes/profile';
import { type NavItem } from '@/types';
import { Link, router, usePage } from '@inertiajs/vue3';
import { computed } from 'vue';
import AppLogo from './AppLogo.vue';

const mainNavItems: NavItem[] = [
    {
        label: 'Dashboard',
        to: dashboard(),
        icon: 'i-lucide-layout-grid',
    },
];

const footerNavItems: NavItem[] = [
    {
        label: 'Github Repo',
        to: 'https://github.com/laravel/vue-starter-kit',
        icon: 'i-lucide-folder',
    },
    {
        label: 'Documentation',
        to: 'https://laravel.com/docs/starter-kits#vue',
        icon: 'i-lucide-book-open',
    },
];

const page = usePage();
const auth = computed(() => page.props.auth);

const userMenuItems = computed(() => [
    [
        {
            label: auth.value.user.name,
            slot: 'account',
            disabled: true,
        },
    ],
    [
        {
            label: 'Settings',
            icon: 'i-lucide-settings',
            to: edit(),
        },
    ],
    [
        {
            label: 'Log out',
            icon: 'i-lucide-log-out',
            click: () => {
                router.post(logout());
            },
        },
    ],
]);
</script>

<template>
    <div class="flex h-full flex-col gap-y-4">
        <div class="flex h-16 shrink-0 items-center border-b px-6">
            <Link :href="dashboard()">
                <AppLogo />
            </Link>
        </div>
        <nav class="flex flex-1 flex-col gap-y-7 px-6">
            <ul role="list" class="flex flex-1 flex-col gap-y-7">
                <li>
                    <ul role="list" class="-mx-2 space-y-1">
                        <li v-for="item in mainNavItems" :key="item.label">
                            <UButton :to="item.to" variant="ghost" color="gray" class="w-full justify-start" :icon="item.icon">
                                {{ item.label }}
                            </UButton>
                        </li>
                    </ul>
                </li>
                <li class="mt-auto">
                    <ul role="list" class="-mx-2 space-y-1">
                        <li v-for="item in footerNavItems" :key="item.label">
                            <UButton
                                :to="item.to"
                                target="_blank"
                                rel="noopener noreferrer"
                                variant="ghost"
                                color="gray"
                                class="w-full justify-start"
                                :icon="item.icon"
                            >
                                {{ item.label }}
                            </UButton>
                        </li>
                    </ul>
                    <UDropdown :items="userMenuItems">
                        <UButton
                            variant="ghost"
                            color="gray"
                            class="relative mt-4 w-full justify-start p-1 focus-within:ring-2 focus-within:ring-primary"
                        >
                            <UAvatar :src="auth.user.avatar" :alt="auth.user.name">
                                <UAvatar
                                    :alt="getInitials(auth.user?.name)"
                                    class="rounded-lg bg-neutral-200 font-semibold text-black dark:bg-neutral-700 dark:text-white"
                                />
                            </UAvatar>
                            <span class="ml-2 text-sm font-semibold">{{ auth.user.name }}</span>
                        </UButton>
                        <template #account>
                            <div class="text-left">
                                <p>Signed in as</p>
                                <p class="truncate font-medium text-gray-900 dark:text-white">
                                    {{ auth.user.email }}
                                </p>
                            </div>
                        </template>
                    </UDropdown>
                </li>
            </ul>
        </nav>
    </div>
</template>
