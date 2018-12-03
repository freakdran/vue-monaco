<template>
  <div id="container"></div>
</template>

<script>
import * as monaco from 'monaco-editor';

export default {
  name: 'monaco-editor-vue',
  props: {
    value: {
      type: String,
      required: true,
    },
    language: {
      type: String,
      default: 'javascript',
    },
    options: {},
    width: {
      type: String,
      default: '100%',
    },
    height: {
      type: String,
      default: '100',
    },
    readOnly: {
      type: Boolean,
      default: false,
    },
    minimapOptions: {
      type: Object,
      default: () => {
        return { enabled: true, force: false, lines: 40 };
      },
    },
    foldOptions: {
      type: Object,
      default: () => {
        return { foldDepth: -1, lines: -1 };
      },
    },
    theme: {
      type: String,
      default: 'vs-light',
    },
    autoLayout: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {
      codeModel: '',
      editor: null,
      changeEvent: null,
    };
  },

  model: {
    event: 'change',
  },

  watch: {
    value: function(newCode) {
      this.codeModel = newCode;
    },
  },
  methods: {},
  computed: {
    showMinimap() {
      return this.minimapOptions.enabled ? (this.minimapOptions.force ? true : this.minimapOptions.lines < this.lineCount) : false;
    },
    lineCount() {
      const lineCount = this.editor.getModel().getLineCount();
      return lineCount;
    },
    foldCode() {
      if (this.foldOptions.foldDepth !== -1 && this.foldOptions.lines !== -1 && this.foldOptions.lines <= this.lineCount) return true;
      else return false;
    },
  },
  async mounted() {
    this.editor = monaco.editor.create(document.getElementById('container'), {
      value: this.value,
      language: this.language,
      theme: this.theme,
      readOnly: this.readOnly,
      scrollBeyondLastLine: false,
      automaticLayout: this.autoLayout,
    });
    this.editor.updateOptions(this.options);
    this.editor.updateOptions({ minimap: { enabled: this.showMinimap } });

    this.editor.onDidChangeModelContent((event) => {
      this.editor.updateOptions({ minimap: { enabled: this.showMinimap } });
      const value = this.editor.getValue();
      if (this.value !== value) {
        this.$emit('change', value, event);
      }
    });
    await setTimeout(function() {}, 1);
    if (this.foldCode) this.editor.getAction(`editor.foldLevel${this.foldOptions.foldDepth}`).run();
  },
};
</script>

<style scoped>
#container {
  height: 100%;
  width: 100%;
}
</style>
