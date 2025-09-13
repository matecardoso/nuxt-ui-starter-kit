<script setup lang="ts">
import AppLogo from '@/components/AppLogo.vue';
import AppLogoIcon from '@/components/AppLogoIcon.vue';
import Breadcrumbs from '@/components/Breadcrumbs.vue';
import { getInitials } from '@/composables/useInitials';
import { toUrl, urlIsActive } from '@/lib/utils';
import { dashboard, logout } from '@/routes';
import { edit } from '@/routes/profile';
import type { BreadcrumbItem, NavItem } from '@/types';
import { InertiaLinkProps, Link, router, usePage } from '@inertiajs/vue3';
import { computed, ref } from 'vue';

interface Props {
    breadcrumbs?: BreadcrumbItem[];
}

const props = withDefaults(defineProps<Props>(), {
    breadcrumbs: () => [],
});

const page = usePage();
const auth = computed(() => page.props.auth);
const isMobileMenuOpen = ref(false);

const isCurrentRoute = computed(() => (url: NonNullable<InertiaLinkProps['href']>) => urlIsActive(url, page.url));

const mainNavItems: NavItem[] = [
    {
        label: 'Dashboard',
        to: dashboard(),
        icon: 'i-lucide-layout-grid',
    },
];

const rightNavItems: NavItem[] = [
    {
        label: 'Repository',
        to: 'https://github.com/laravel/vue-starter-kit',
        icon: 'i-lucide-folder',
    },
    {
        label: 'Documentation',
        to: 'https://laravel.com/docs/starter-kits#vue',
        icon: 'i-lucide-book-open',
    },
];

const handleLogout = () => {
    router.post(logout());
};

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
            click: handleLogout,
        },
    ],
]);
</script>

<template>
    <div>
        <div class="border-b border-gray-200 dark:border-gray-800">
            <div class="mx-auto flex h-16 items-center px-4 md:max-w-7xl">
                <!-- Mobile Menu -->
                <div class="lg:hidden">
                    <UButton
                        variant="ghost"
                        color="gray"
                        icon="i-lucide-menu"
                        class="mr-2"
                        @click="isMobileMenuOpen = true"
                    />

                    <USlideover v-model="isMobileMenuOpen">
                        <div class="p-6">
                            <div class="flex justify-start text-left">
                                <AppLogoIcon class="size-6 fill-current text-black dark:text-white" />
                            </div>
                            <div class="flex h-full flex-1 flex-col justify-between space-y-4 py-6">
                                <nav class="-mx-3 space-y-1">
                                    <UButton
                                        v-for="item in mainNavItems"
                                        :key="item.label"
                                        :to="item.to"
                                        variant="ghost"
                                        color="gray"
                                        class="w-full justify-start"
                                        :icon="item.icon"
                                    >
                                        {{ item.label }}
                                    </UButton>
                                </nav>
                                <div class="flex flex-col space-y-4">
                                    <UButton
                                        v-for="item in rightNavItems"
                                        :key="item.label"
                                        :to="toUrl(item.to)"
                                        target="_blank"
                                        rel="noopener noreferrer"
                                        variant="ghost"
                                        color="gray"
                                        class="w-full justify-start"
                                        :icon="item.icon"
                                    >
                                        {{ item.label }}
                                    </UButton>
                                </div>
                            </div>
                        </div>
                    </USlideover>
                </div>

                <Link :href="dashboard()" class="flex items-center gap-x-2">
                    <AppLogo />
                </Link>

                <!-- Desktop Menu -->
                <div class="hidden h-full lg:flex lg:flex-1">
                    <UHorizontalNavigation :links="mainNavItems" class="ml-10" />
                </div>

                <div class="ml-auto flex items-center space-x-2">
                    <div class="relative flex items-center space-x-1">
                        <UButton variant="ghost" color="gray" icon="i-lucide-search" />

                        <div class="hidden space-x-1 lg:flex">
                            <template v-for="item in rightNavItems" :key="item.label">
                                <UTooltip :text="item.label">
                                    <UButton
                                        :to="toUrl(item.to)"
                                        target="_blank"
                                        rel="noopener noreferrer"
                                        variant="ghost"
                                        color="gray"
                                        :icon="item.icon"
                                    />
                                </UTooltip>
                            </template>
                        </div>
                    </div>

                    <UDropdown :items="userMenuItems">
                        <UButton
                            variant="ghost"
                            color="gray"
                            class="relative size-10 w-auto rounded-full p-1 focus-within:ring-2 focus-within:ring-primary"
                        >
                            <UAvatar
                                :src="auth.user.avatar"
                                :alt="auth.user.name"
                            >
                                <UAvatar
                                    :alt="getInitials(auth.user?.name)"
                                    class="rounded-lg bg-neutral-200 font-semibold text-black dark:bg-neutral-700 dark:text-white"
                                />
                            </UAvatar>
                        </UButton>
                        <template #account="{ item }">
                            <div class="text-left">
                                <p>Signed in as</p>
                                <p class="truncate font-medium text-gray-900 dark:text-white">
                                    {{ auth.user.email }}
                                </p>
                            </div>
                        </template>
                    </UDropdown>
                </div>
            </div>
        </div>

        <div v-if="props.breadcrumbs.length > 1" class="flex w-full border-b border-gray-200 dark:border-gray-800">
            <div class="mx-auto flex h-12 w-full items-center justify-start px-4 text-neutral-500 md:max-w-7xl">
                <Breadcrumbs :breadcrumbs="breadcrumbs" />
            </div>
        </div>
    </div>
</template>
