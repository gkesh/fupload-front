<template>
  <div class="history-box">
    <div class="history-blade">
      <div class="history-title">
        {{ title }}
        <span>{{ extension }}</span>
      </div>
      <div class="history-date">
        {{ dateUploaded }}
      </div>
    </div>
    <div class="preview"></div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "HistoryBox",
  props: {
    title: {
      type: String,
    },
    filename: {
      type: String,
    },
    extension: {
      type: String,
    },
    dateUploaded: {
      type: String,
    },
  },
});
</script>

<style lang="scss" scoped>
.history-box {
  margin: 10px 20px;
  padding: 30px 0;

  &:first-of-type {
    margin-top: 0px;
  }

  &:not(:first-of-type) {
    border-top: 1px solid var(--primary);
  }

  &:last-of-type {
    margin-bottom: 0px;
  }
  .history-blade {
    display: flex;
    flex-direction: row;
    justify-content: space-between;

    .history-title {
      color: var(--primary);
      font-size: 1.05em;

      span {
        margin-left: 12px;
        font-size: 0.8em;
        padding: 4px 8px;
        border-radius: 8px;
        background: var(--primary);
        color: white;
      }
    }
  }
}
</style>
