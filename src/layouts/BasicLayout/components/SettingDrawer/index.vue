<template>
  <n-drawer v-model:show="app.settingDrawer.visible" :width="330">
    <n-drawer-content title="主题配置" :native-scrollbar="false">
      <dark-mode />
      <nav-mode />
      <system-theme />
      <page-func />
      <page-view />
      <theme-config />
    </n-drawer-content>
  </n-drawer>
</template>

<script lang="ts" setup>
import { NDrawer, NDrawerContent } from 'naive-ui';
import { useAppStore } from '@/store';
import { DarkMode, NavMode, SystemTheme, PageFunc, PageView, ThemeConfig } from './components';

const app = useAppStore();
</script>
<style scoped></style>
