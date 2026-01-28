<script setup>
import FlowIconBtn from "./FlowIconBtn.vue";
</script>

<template>
  <div class="row no-wrap q-gutter-x-xs">
    <div class="text-white q-px-sm rounded-borders shadow-1 q-mr-md">
      <div class="fit column items-center justify-center text-weight-bold" style="cursor: pointer">
        타이머
      </div>
    </div>
    <FlowIconBtn
      label="걸기"
      class="q-mr-xs"
      icon="phone_forwarded"
    />
    <FlowIconBtn label="끊기" class="q-mr-xs" icon="call_end" />
    <FlowIconBtn label="대기" class="q-mr-xs" icon="hourglass_empty" />
    <FlowIconBtn
      label="보류"
      icon="watch_later"
      class="q-mr-xs"
    />
    <FlowIconBtn
      label="호전환"
      icon="timeline"
      style="margin-right: 11px"
    />
    <FlowIconBtn
      label="휴식"
      icon="local_cafe"
      class="q-mr-xs"
    />
    <FlowIconBtn
      label="교육"
      icon="school"
      class="q-mr-xs"
    />
    <FlowIconBtn
      label="공무"
      icon="work"
      class="q-mr-xs"
    />
    <FlowIconBtn
      label="식사"
      icon="restaurant"
      class="q-mr-xs"
    />
  </div>
</template>

<style lang="scss" scoped>
.GREEN {
  background-color: #325a32;
}
</style>
