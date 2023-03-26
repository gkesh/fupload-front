<template>
  <main>
    <section class="upload">
      <div class="nothing" v-if="fileCount === 0">
        No files selected. Please click the "More" button to get started.
      </div>
      <UploadBox
        v-else
        v-for="serialNo in files"
        :index="serialNo"
        :key="serialNo"
        @on-remove="deleteFile"
      />
    </section>
    <section class="actions">
      <button type="button" class="success">Upload</button>
      <button type="button" class="more" @click="incrementFileCount">
        More
      </button>
      <button
        v-if="fileCount > 0"
        type="button"
        class="error"
        @click="clearFiles"
      >
        Clear
      </button>
    </section>
  </main>
</template>

<script lang="ts">
import { defineComponent, ref, Ref } from "vue";
import UploadBox from "./components/UploadBox.vue";

export default defineComponent({
  name: "App",
  components: {
    UploadBox,
  },
  setup() {
    const fileCount: Ref<number> = ref(0);
    const files: Ref<number[]> = ref([]);

    const incrementFileCount = (): void => {
      fileCount.value = fileCount.value + 1;
      files.value[files.value.length] = fileCount.value;
    };

    const deleteFile = (id: number): void => {
      files.value = files.value.filter((item) => item !== id);
      console.log(files.value, id);
    };

    const clearFiles = (): void => {
      fileCount.value = 0;
      files.value = [];
    };

    return {
      files,
      fileCount,
      clearFiles,
      deleteFile,
      incrementFileCount,
    };
  },
});
</script>

<style lang="scss">
:root {
  --primary: #6d5e79;
  --success: #436f49;
  --error: #5f2828;
  --backgroundPrimary: #dbc3ed;
  --backgroundSuccess: #9befbc;
  --backgroundError: #ed7855;
  --backgroundLight: #f2f2f2;

  --border: #e3e3e3;
  --text: #2c3e50;
}

* {
  font-family: Ubuntu, Avenir, Helvetica, Arial, sans-serif;
  font-weight: 500;
  box-sizing: border-box;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: var(--text);
}

main {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem;

  section {
    width: 600px;
    max-width: 100%;
    margin-bottom: 2rem;
    border-radius: 24px;

    .nothing {
      margin: 24px 0;
      font-style: italic;
    }

    &.upload {
      background: var(--backgroundLight);

      & > .upload-box:not(:first-of-type) {
        border-top: 1px solid var(--border);
      }
    }

    &.actions {
      display: flex;
      flex-direction: row;
      justify-content: center;
      gap: 20px;
    }
  }

  input,
  button {
    padding: 12px 24px;
    border-radius: 12px;
    border: none;
    cursor: pointer;

    &.primary {
      background: var(--backgroundPrimary);
      color: var(--primary);
    }

    &.error {
      background: var(--backgroundError);
      color: var(--error);
    }

    &.success {
      background: var(--backgroundSuccess);
      color: var(--success);
    }
  }
}
</style>
