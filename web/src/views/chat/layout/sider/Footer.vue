<script setup lang='ts'>
import { defineAsyncComponent, ref } from 'vue'
import { HoverButton, SvgIcon, UserAvatar } from '@/components/common'
import { useAppStore, useAuthStore, useChatStore, useUserStore } from '@/store/modules'

const Setting = defineAsyncComponent(() => import('@/components/common/Setting/index.vue'))

const authStore = useAuthStore()
const userStore = useUserStore()
const chatStore = useChatStore()
const appStore = useAppStore()

const show = ref(false)

function handleLogout() {
  // clear all stores
  authStore.removeToken()
  userStore.resetUserInfo()
  chatStore.clearState()
}

function handleChangelang() {
  appStore.setNextLanguage()
}
</script>

<template>
  <footer class="flex items-center justify-between min-w-0 p-4 overflow-hidden border-t dark:border-neutral-800">
    <div class="flex-1 flex-shrink-0 overflow-hidden">
      <UserAvatar />
    </div>
    <HoverButton :tooltip="$t('common.logout')" @click="handleLogout">
      <span class="text-xl text-[#4f555e] dark:text-white">
        <SvgIcon icon="ri:logout-circle-r-line" />
      </span>
    </HoverButton>

    <HoverButton :tooltip="$t('setting.setting')" @click="show = true">
      <span class="text-xl text-[#4f555e] dark:text-white">
        <SvgIcon icon="ri:settings-4-line" />
      </span>
    </HoverButton>
    <Setting v-if="show" v-model:visible="show" />
  </footer>
</template>
