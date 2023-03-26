<template>
  <div class="upload-box">
    <span class="serial">{{ index }}</span>
    <input type="file" :name="'file-' + index" />
    <button type="button" class="error" @click="emitRemove(index)">
      Remove
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "UploadBox",
  props: {
    index: {
      type: Number,
      default: 0,
    },
  },
  emits: ["on-remove"],
  setup(_, { emit }) {
    const emitRemove = (index: number): void => {
      emit("on-remove", index);
    };

    return {
      emitRemove,
    };
  },
});
</script>

<style lang="scss" scoped>
.upload-box {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  gap: 12px;
  padding: 20px;

  .serial {
    width: 50px;
    padding: 12px;
    border-radius: 12px;
    font-weight: 900;
    background: var(--backgroundPrimary);
    color: var(--primary);
  }
}
</style>
