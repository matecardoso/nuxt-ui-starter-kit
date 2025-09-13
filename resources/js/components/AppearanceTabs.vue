<script setup lang="ts">
import { useAppearance } from '@/composables/useAppearance';

const { appearance, updateAppearance } = useAppearance();

const items = [
    { key: 'light', label: 'Light', icon: 'i-lucide-sun' },
    { key: 'dark', label: 'Dark', icon: 'i-lucide-moon' },
    { key: 'system', label: 'System', icon: 'i-lucide-monitor' },
];

const onTabChange = (index: number) => {
    updateAppearance(items[index].key);
};
</script>

<template>
    <UTabs
        :model-value="items.findIndex((item) => item.key === appearance)"
        @update:model-value="onTabChange"
        :items="items"
        class="w-full"
    >
        <template #default="{ item, index, selected }">
            <div
                class="relative flex items-center gap-2 truncate"
                :class="[selected ? 'text-primary' : 'text-gray-500 dark:text-gray-400', 'group-hover:text-primary']"
            >
                <UIcon :name="item.icon" class="size-4" />
                <span class="truncate">{{ item.label }}</span>
            </div>
        </template>
    </UTabs>
</template>
