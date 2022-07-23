<template>
    <div :class="['level-'+level]">
        <div class="entry">
            <folder-knob v-model="$data._collapsed"/>
            <span-editable ref="name" class="name">{{entry.displayName || entry.name}}</span-editable>
        </div>
        <file-list ref="l" :files="entry.files" :path="_path" :level="level"
                   :selection_="subselection(selection, entry.name)"
                   v-show="!$data._collapsed"
                   @action="$emit('action', $event)">
        </file-list>
    </div>
</template>

<script>
import FolderKnob from './folder-knob.vue';
import SpanEditable from './span-editable.vue';

/**
 * `<file-list.folder>`
 * Represents a subfolder.
 */
export default {
    props: ['entry', 'level', 'path', 'selection', 'collapsed'],
    data: function() { return {
        _collapsed: !!this.collapsed
    }; },
    computed: {
        _path() { return [...(this.path || []), this.entry.name]; }
    },
    methods: {
        subselection(selection, folder_name) {
            if (selection) {
                return selection.filter(x => x[0] === folder_name)
                                .map(x => x.slice(1));
            }
        },
        renameStart() { this.$refs.name.edit(); },
        rename(v) {
            if (v != this.entry.name)
                this.$emit('action', {type: 'rename', from: this.entry.name, to: v});
        }
    },
    components: {
        'file-list': () => import('./index.vue'),   // recursion!
        FolderKnob, SpanEditable
    }
}
</script>