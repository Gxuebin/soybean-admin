<template>
  <hover-container class="w-40px h-full" placement="bottom-end" content="项目配置" @click="openSettingDrawer">
    <icon-mdi-light-cog class="text-16px" />
  </hover-container>
</template>

<script lang="ts" setup>
import { useAppStore } from '@/store';
import { HoverContainer } from '@/components';

const { openSettingDrawer } = useAppStore();
</script>
<style scoped></style>
