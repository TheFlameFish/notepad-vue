<script lang="ts">
    export default {
        props: {
            path: String,
            content: String
        },
        data() {
            return {
                lines: 0,
                characters: 0
            }
        },
        watch: {
            content(newContent: String) {
                this.characters = newContent.length;
                this.lines = newContent.split('\n').length;
            }
        }
    }
</script>

<template>
    <div class="footer">
        {{ path || 'No file open' }}&emsp;Lines: {{ lines }}&emsp;Characters: {{ characters }}
    </div> 
</template>