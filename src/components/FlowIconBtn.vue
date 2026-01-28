<script setup>
defineProps({ label: String, icon: String, disable: Boolean });
</script>

<template>
  <q-btn class="FlowIconBtn" :disable="$props.disable">
    <slot></slot>
    <div class="">
      <q-icon
        :class="{
          'text-grey-7': $props.disable,
          'text-primary': !$props.disable,
        }"
        :name="$props.icon"
      />
      <div style="font-size: 13px">{{ $props.label }}</div>
    </div>
  </q-btn>
</template>

<style lang="scss" scoped>
.FlowIconBtn {
  padding: 3px;
  width: 55px;
  height: 51px;
}

.FlowIconBtn.disabled {
  background-color: $grey-3;
}
</style>
