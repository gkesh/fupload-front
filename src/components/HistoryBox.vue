<template>
  <div class="history-box">
    <h1>{{ title }}</h1>
    <p>{{ filename }}</p>
    <span>{{ extension }}</span>
    <p>{{ dateUploaded }}</p>
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
      type: Date,
    },
  },
});
</script>
