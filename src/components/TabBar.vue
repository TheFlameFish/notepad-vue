<script lang="ts">
    export default {
        props: {
            files: {
                type: Array as () => Array<{ path?: string, content?: string }>,
                required: true
            },
            openIndex: Number
        },
        emits: [
            'changeTab',
            'closeTab'
        ],
        methods: {
            getSimplifiedPath(path: String | undefined) {
                if (typeof(path) == 'string') {
                    const pathSplit = path.split('/');
                    return pathSplit[pathSplit.length - 1]
                } else {
                    return 'New file'
                }
            }
        }
    }
</script>

<template>
    <div class="tabBar">
        <div v-for="(file, index) in files">
            <div v-if="file.content != undefined" :class="openIndex == index ? 'openTab' : 'tab'" >
                <div @click="$emit('changeTab', index)">{{ getSimplifiedPath(file.path) }}</div>
                <button class="tabClose" @click="$emit('closeTab', index)">X</button>
            </div>
        </div>
    </div>
</template>