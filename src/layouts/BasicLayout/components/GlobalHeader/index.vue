<template>
  <header v-if="fixedHeaderAndTab && theme.navStyle.mode !== 'horizontal-mix'" class="header-height w-full"></header>
  <n-layout-header :inverted="headerInverted" :position="position" :style="{ zIndex }">
    <div class="global-header header-height flex-y-center w-full">
      <div v-if="!theme.isVerticalNav" class="menu-width h-full">
        <global-logo />
      </div>
      <div v-if="theme.navStyle.mode !== 'horizontal'" class="flex-1-hidden flex-y-center h-full">
        <menu-collapse v-if="theme.navStyle.mode !== 'vertical-mix'" />
        <global-breadcrumb v-if="theme.crumbsStyle.visible" />
      </div>
      <div
        v-else
        class="flex-1-hidden flex-y-center h-full"
        :style="{ justifyContent: theme.menuStyle.horizontalPosition }"
      >
        <header-menu />
      </div>
      <div class="flex justify-end h-full">
        <gihub-site />
        <full-screen />
        <theme-mode />
        <user-avatar />
        <setting-drawer-button v-if="showSettingButton" />
      </div>
    </div>
  </n-layout-header>
</template>

<script lang="ts" setup>
import { computed } from 'vue';
import { NLayoutHeader } from 'naive-ui';
import { useThemeStore } from '@/store';
import {
  GlobalBreadcrumb,
  UserAvatar,
  MenuCollapse,
  ThemeMode,
  FullScreen,
  GihubSite,
  SettingDrawerButton
} from './components';
import { GlobalLogo } from '../common';
import HeaderMenu from './components/HeaderMenu.vue';

interface Props {
  /** 层级z-index */
  zIndex?: number;
}

withDefaults(defineProps<Props>(), {
  zIndex: 0
});

const theme = useThemeStore();

const inverted = computed(() => {
  return theme.navStyle.theme !== 'light';
});
const fixedHeaderAndTab = computed(() => theme.fixedHeaderAndTab || theme.navStyle.mode === 'horizontal-mix');
const position = computed(() => (fixedHeaderAndTab.value ? 'absolute' : 'static'));
const headerInverted = computed(() => {
  return theme.navStyle.theme !== 'dark' ? inverted.value : !inverted.value;
});
const headerHeight = computed(() => {
  const { height } = theme.headerStyle;
  return `${height}px`;
});
const menuWidth = computed(() => {
  const { width } = theme.menuStyle;

  return `${width}px`;
});

const showSettingButton = import.meta.env.DEV || import.meta.env.VITE_HTTP_ENV === 'STAGING';
</script>
<style scoped>
.global-header {
  box-shadow: 0 1px 4px rgb(0 21 41 / 8%);
}
.header-height {
  height: v-bind(headerHeight);
}
.menu-width {
  width: v-bind(menuWidth);
}
</style>
