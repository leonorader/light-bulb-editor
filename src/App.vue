<template>
  <div id="app">
    <BlocklyComponent id="blockly2" :options="options" ref="editor"></BlocklyComponent>
    <p id="code">
      <!--<button v-on:click="showCode()">Show JavaScript</button>-->
      <button v-on:click="runCode()">Run code</button>
      <pre v-html="code"></pre>
    </p>
  </div>
</template>

<script>

import BlocklyComponent from './components/BlocklyComponent.vue'
import './blocks/light-bulb';
import './prompt';

import BlocklyJS from 'blockly/javascript';

export default {
  name: 'app',
  components: {
    BlocklyComponent
  },
  data(){
    return {
      code: '',
      options: {
        media: 'media/',
        grid:
          {
            spacing: 25,
            length: 3,
            colour: '#ccc',
            snap: true
          },
        toolbox:
        `<xml>
          <category name="Logic" colour="%{BKY_LOGIC_HUE}">
            <block type="controls_if"></block>
            <block type="logic_compare"></block>
            <block type="logic_operation"></block>
            <block type="logic_negate"></block>
            <block type="logic_boolean"></block>
          </category>
          <category name="Loops" colour="%{BKY_LOOPS_HUE}">
            <block type="controls_repeat_ext">
              <value name="TIMES">
                <block type="math_number">
                  <field name="NUM">10</field>
                </block>
              </value>
            </block>
            <block type="controls_whileUntil"></block>
          </category>
          <category name="Math" colour="%{BKY_MATH_HUE}">
            <block type="math_number">
              <field name="NUM">123</field>
            </block>
            <block type="math_arithmetic"></block>
            <block type="math_single"></block>
          </category>
          <category name="Text" colour="%{BKY_TEXTS_HUE}">
            <block type="text"></block>
            <block type="text_length"></block>
            <block type="text_print"></block>
          </category>
          <category name="Variables" custom="VARIABLE" colour="%{BKY_VARIABLES_HUE}">
            </category>
          <category name="Light bulb" colour="%{BKY_LOOPS_HUE}">
            <block type="set_light_bulb_color"></block>
            <block type="turn_light_bulb"></block>
          </category>
        </xml>`
      }
    }
  },
  computed: {
    // code() {
    //   if (!(this.$refs && this.$refs.editor)) return ''
    //   return BlocklyJS.workspaceToCode(this.$refs["editor"].workspace)
    // }
  },
  methods: {
    runCode() {
      this.code = BlocklyJS.workspaceToCode(this.$refs["editor"].workspace)
      console.log(this.code)
      var F = new Function (this.code);
      return(F());
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

html, body {
  margin: 0;
}

#code {
  position: absolute;
  right: 0;
  bottom: 0;
  width: 50%;
  height: 50%;
  margin: 0;
  background-color: beige;
}

#blockly1 {
  position: absolute;
  right: 0;
  top: 0;
  width: 50%;
  height: 50%;
}

#blockly2 {
  position: absolute;
  left: 0;
  bottom: 0;
  width: 50%;
  height: 50%;
}
</style>
