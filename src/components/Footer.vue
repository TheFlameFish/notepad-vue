<script lang="ts">
    export default {
        props: {
            path: String,
            content: {
                type: String,
                default: undefined
            }
        },
        data() {
            return {
                lines: 0,
                characters: 0
            }
        },
        watch: {
            content(newContent: String) {
                if (this.content != undefined) {
                    this.characters = newContent.length;
                    this.lines = newContent.split('\n').length;
                } else {
                    this.characters = 0;
                    this.lines = 0;
                }
            }
        }
    }
</script>

<template>
    <div class="footer">
        {{ path || 'No file open' }}&emsp;&emsp;Lines: {{ lines }}&emsp;&emsp;Characters: {{ characters }}
    </div> 
</template>