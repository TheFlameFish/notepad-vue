<script lang="ts">
  import Editor from './components/Editor.vue';
import Footer from './components/Footer.vue';
  export default {
    components: {
      Editor,
      Footer
    },
    data() {
      return {
        files: [
          {
            path: undefined,
            content: ""
          }
        ],
        openFile: 0
      }
    }
  }
</script>

<template>
  <Editor v-model="files[openFile].content">Cheese</Editor>
  <Footer :path="files[openFile].path" :content="files[openFile].content"/>
</template>

<style lang="less">
  @import "./assets/.less";
</style> 