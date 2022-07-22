<template>
    <div class="entry">
        <span-editable ref="name" class="name" @input="rename">{{entry.name}}</span-editable>
        <tags :tags="entry.tags"/>
    </div>    
</template>

<script>
import SpanEditable from './span-editable.vue';
import Tags from './tags.vue';

/**
 * `<file-list.file>`
 * Represents a file entry.
 */
export default {
    props: ['entry'],
    methods: {
        renameStart() { this.$refs.name.edit(); },
        rename(v) {
            if (v != this.entry.name)
                this.$emit('action', {type: 'rename', from: this.entry.name, to: v});
        }
    },
    components: { SpanEditable, Tags }
}
</script>