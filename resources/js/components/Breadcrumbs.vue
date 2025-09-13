<script setup lang="ts">
import { Link } from '@inertiajs/vue3';
import { computed } from 'vue';

interface BreadcrumbItemType {
    title: string;
    href?: string;
}

const props = defineProps<{
    breadcrumbs: BreadcrumbItemType[];
}>();

const links = computed(() =>
    props.breadcrumbs.map((item) => ({
        label: item.title,
        to: item.href,
        // icon: 'i-heroicons-home',
    })),
);
</script>

<template>
    <UBreadcrumb :links="links" />
</template>
