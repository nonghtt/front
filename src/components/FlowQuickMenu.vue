<script setup>

const quickMenuItems = [
  {name: "테스트1", iconUrl: "assets/default-icon-set/ACCESS_LOG_MANAGEMENT.svg"},
  {name: "테스트2", iconUrl: "assets/default-icon-set/ACCESS_LOG_MANAGEMENT.svg"},
]
</script>

<template>
  <q-drawer :model-value="true" behavior="desktop" :width="50" bordered>
    <q-scroll-area class="fit">
      <div class="column items-center q-py-sm">
        <div v-for="item in quickMenuItems" :key="item.name" class="q-ma-sm cursor-pointer">
          <div>
            <img :src="item.iconUrl" alt="icon" style="width: 24px; height: 24px" />
            <q-tooltip anchor="center end" self="center start">{{ item.name }}</q-tooltip>
          </div>
         
        </div>
      </div>
    </q-scroll-area>
  </q-drawer>
</template>

<style lang="scss" scoped></style>
