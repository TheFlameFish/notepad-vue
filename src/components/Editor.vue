<script lang="ts">
export default {
  props: {
    modelValue: String
  },
  methods: {
    updateValue(event: Event) {
      const target = event.target as HTMLTextAreaElement;
      this.$emit('update:modelValue', target.value);
    },
    handle_key(event: Event) {
      const key = (event as KeyboardEvent).key;
      if (key == "Tab") {
        const input = event.target as HTMLTextAreaElement;
        input.setRangeText(
          '\t',
          input.selectionStart,
          input.selectionEnd,
          "end"
        );

        // Prevent default behaviour
        event.preventDefault();
        return false;
      }
    }
  }
}
</script>

<template>
    <div v-if="modelValue != undefined" class="editor">
        <textarea autofocus :value="modelValue" @keydown="handle_key" @input="updateValue"></textarea>
    </div>
    <div v-else class="editor-null"/>
</template> 
