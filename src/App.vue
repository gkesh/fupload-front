<template>
  <main>
    <section class="upload">
      <UploadBox
        v-for="serialNo in files"
        :index="serialNo"
        :key="serialNo"
        @on-remove="deleteFile"
      />
    </section>
    <section>
      <button class="more" type="button" @click="incrementFileCount">
        More
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
    const fileCount: Ref<number> = ref(1);
    const files: Ref<number[]> = ref([1]);

    const incrementFileCount = (): void => {
      fileCount.value = fileCount.value + 1;
      files.value[files.value.length] = fileCount.value;
    };

    const deleteFile = (id: number): void => {
      files.value = files.value.filter((item) => item !== id);
      console.log(files.value, id);
    };

    return {
      files,
      deleteFile,
      incrementFileCount,
    };
  },
});
</script>

<style lang="scss">
:root {
  --primary: #6d5e79;
  --backgroundPrimary: #dbc3ed;
  --backgroundLight: #f2f2f2;

  --border: #e3e3e3;

  --error: #ed7855;
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

    &.upload {
      background: var(--backgroundLight);

      & > .upload-box:not(:first-of-type) {
        border-top: 1px solid var(--border);
      }
    }
  }

  input,
  button {
    padding: 12px 24px;
    border-radius: 12px;
    border: none;
    cursor: pointer;
  }
}
</style>
