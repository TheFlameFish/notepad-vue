<script lang="ts">
  import Editor from './components/Editor.vue';
  import Footer from './components/Footer.vue';
  import TabBar from './components/TabBar.vue';

  import { Menu, MenuItem, Submenu } from '@tauri-apps/api/menu';

  export default {
    components: {
      Editor,
      Footer,
      TabBar,
    },
    data() {
      return {
        files: [
          {
            path: "",
            content: undefined,
            id: -1
          },
          {
            path: "Onions",
            content: "Onions, yay.",
            id: 0
          },
          {
            path: "Not Onions",
            content: "No onions, sad.",
            id: 1
          },
          {
            path: "~/Documents/Cool stuff/bird.txt",
            content: "Birds are cool! I love birds!",
            id: 2
          },
          {
            path: undefined,
            content: "",
            id: 3
          }
        ],
        openFile: 0,
        nextId: 4
      }
    },
    methods: {
      newFile() {
        this.files.push({
          path: undefined,
          content: '',
          id: this.nextId
        })
        this.openFile = this.files.length - 1;
        this.nextId++;
      },
      closeTab(index: number) {
        let open_id = this.files[this.openFile].id;
        
        if (open_id == this.files[index].id) {
          
        }
      }
    },
    async created() {
      // Primary submenu
      const primarySubmenu = await Submenu.new({
        id: 'primary-menu',
        text: '',
        items: []
      })

      // File submenu
      const newFileItem = await MenuItem.new({
        id: 'new-file',
        text: 'New File',
        action: () => this.newFile(),
      });
      const openFileItem = await MenuItem.new({
        id: 'open-file',
        text: 'Open File',
        action: () => console.log('Open File clicked'),
      });

      const fileSubmenu = await Submenu.new({
        id: 'file-menu',
        text: 'File',
        items: [newFileItem, openFileItem],
      });

      const mainMenu = await Menu.new({
        items: [primarySubmenu, fileSubmenu],
      });

      // Set the menu as the global app menu
      await mainMenu.setAsAppMenu();
    }
  }
</script>

<template>
  <TabBar :files="files" :open-index="openFile" @changeTab="(index: number) => {openFile = index}" @close-tab=""/>
  <Editor v-model="files[openFile].content">Cheese</Editor>
  <Footer :path="files[openFile].path" :content="files[openFile].content"/>
</template>

<style lang="less">
  @import "./assets/.less";
</style> 