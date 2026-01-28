<script setup>
import MenuBtn from "components/MenuBtn.vue";
import SoftPhone from "components/SoftPhone2.vue";
</script>

<template>
  <q-header class="flow-header-shadow">
    <div class="FlowHeader q-px-sm row items-center no-wrap">
      <menu-btn flat round :offset="[10, 15]" />

      <img
        class="q-ml-sm col-auto cursor-pointer"
        src="~assets/images/mafra_main_logo.png"
        style="width: 220px; object-fit: fill"
      />

      <q-space />
      <SoftPhone ref="softPhone" />
      <q-space />

      <q-btn class="col-auto q-ml-sm logout-btn" label="로그아웃" color="primary" dense />
    </div>
  </q-header>
</template>

<style lang="scss" scoped>
.flow-header-shadow {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  border-bottom: 1px solid $flow-border-light;
}

.FlowHeader {
  background: linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%);
  color: $flow-text-label;
  height: 67px;
  backdrop-filter: blur(8px);

  .user-info {
    background: rgba(255, 255, 255, 0.7);
    border-radius: 6px;
    padding: 4px 6px;
    border: 1px solid $flow-border-light;
    transition: all 0.2s ease;
    text-align: right;

    .user-name {
      font-size: 12px;
      font-weight: 600;
      color: $flow-text-label;
      line-height: 1.2;
    }

    .user-id {
      font-size: 11px;
      color: $flow-text-secondary;
      line-height: 1.2;
    }

    &:hover {
      background: rgba(255, 255, 255, 0.9);
      border-color: $flow-border;
      transform: translateY(-1px);
    }
  }

  .logout-btn {
    border-radius: 5px;
    font-size: 12px;
    font-weight: 500;
    padding: 6px 12px;
    min-height: 32px;
    transition: all 0.2s ease;

    &:hover {
      transform: translateY(-1px);
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
    }
  }

  :deep(.notification-button) {
    .q-btn {
      min-height: 32px;
      padding: 4px 8px;
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.06);

      .q-btn__content {
        font-size: 12px;

        .q-icon {
          font-size: 18px;
        }
      }

      &:hover {
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.08);
      }
    }
  }

  :deep(.q-btn) {
    // min-height: 32px;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.06);

    .q-btn__content {
      .q-icon {
        font-size: 18px;
      }
    }

    &:hover {
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.08);
    }
  }
}

.notification-button[data-count="0"]::after {
  display: none;
}

.notification-button[data-count]:not([data-count="0"])::after {
  content: attr(data-count);
  position: absolute;
  top: -5px;
  right: -5px;
  background-color: red;
  color: white;
  border-radius: 50%;
  padding: 3px 6px;
  font-size: 0.75rem;
  font-weight: bold;
  line-height: 1;
  min-width: 20px;
  text-align: center;
  box-shadow: 0px 0px 2px rgba(0, 0, 0, 0.5);
}
</style>
