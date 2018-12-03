<template>
  <div id="app">
    <div style="height:500px">
      <MonacoEditorVue
        v-model="code"
        :value="code"
        :options="options"
        :minimapOptions="minimapOptions"
        :foldOptions="foldOptions"
        theme="vs-dark"
      />
    </div>
  </div>
</template>

<script>
import MonacoEditorVue from "../../src/MonacoEditorVue";

export default {
  name: "App",
  components: {
    MonacoEditorVue
  },

  data() {
    return {
      code:
        "// First line\nfunction hello() {\n\talert('Hello world!');\n}\n// Last line",
      /**
       * @param {Boolean} enabled is the minimap enabled
       * @param {Boolean} force is if the minimap is always shown - mandatory if enabled is true
       * @param {Number} lines number of lines when the minimap should not be displayed, e.g. lines:30 -> minimap shown at 31 lines - mandatory if force is false
       */
      minimapOptions: { enabled: true, force: false, lines: 5 },
      /**
       * @param {Number} foldDepth
       * @param {Number} lines number of lines when fold should happen - only if foldDepth is set
       */
      foldOptions: { foldDepth: 1, lines: 3 }
    };
  },
  watch: {
    code: function(val) {
      console.log(val);
    }
  },
  computed: {
    //example options
    options() {
      return {
        readOnly: false,
        scrollBeyondLastLine: false,
        automaticLayout: true
      };
    }
  }
};
</script>

<style>
</style>
