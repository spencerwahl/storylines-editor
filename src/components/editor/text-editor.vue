<template>
    <div class="flex flex-col">
        <label class="text-left">Panel title:</label>
        <input type="text" v-model="panel.title" />
        <label class="text-left">Panel body:</label>
        <v-md-editor
            v-model="panel.content"
            height="400px"
            left-toolbar="undo redo clear | h bold italic strikethrough quote | ul ol table hr | addLink image code | save"
            :toolbar="toolbar"
        ></v-md-editor>
    </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';

@Component({
    components: {}
})
export default class TextEditorV extends Vue {
    @Prop() panel!: any;

    toolbar = {
        addLink: {
            title: 'Insert Link',
            icon: 'v-md-icon-link',
            menus: [
                {
                    name: 'Add External Link',
                    text: 'Add External Link',
                    action(editor: any) {
                        editor.insert((selected: string) => {
                            const content = selected || ``;

                            return {
                                text: `[${content}](http://)`,
                                selected: selected
                            };
                        });
                    }
                },
                {
                    name: 'Add Dynamic Link',
                    text: 'Add Dynamic Link',
                    action(editor: any) {
                        editor.insert((selected: string) => {
                            const content = selected || ``;

                            return {
                                text: `<a panel='panel-id-here'>${content}</a>`,
                                selected: selected
                            };
                        });
                    }
                }
            ]
        }
    };
}
</script>

<style lang="scss" scoped>
label {
    text-align: left !important;
}
</style>
