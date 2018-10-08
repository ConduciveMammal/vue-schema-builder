<template>
  <div class="container">
    <div class="Polaris-Layout">
      <div class="Polaris-Layout__Section Polaris-Layout__Section--secondary">
        <div class="Polaris-Card">
          <form @submit.prevent="addCategory">
            <div class="Polaris-Card__Header">
              <h2 class="Polaris-Heading">Create New Category</h2>
            </div>
            <div class="Polaris-Card__Section">
              <div class="Polaris-FormLayout">
                <div class="Polaris-FormLayout__Item">
                  <div class="">
                    <div class="Polaris-Labelled__LabelWrapper">
                      <div class="Polaris-Label"><label id="CategoryInputLabel" for="CategoryInput" class="Polaris-Label__Text">Category Name</label></div>
                    </div>
                    <div class="Polaris-TextField Polaris-TextField--hasValue">
                      <input id="CategoryInput" class="Polaris-TextField__Input" aria-label="Category Name" aria-labelledby="CategoryInputLabel" aria-invalid="false" v-model="catName">
                      <div class="Polaris-TextField__Backdrop"></div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="Polaris-Card__Footer">
              <div class="Polaris-ButtonGroup">
                <div class="Polaris-ButtonGroup__Item">
                  <button type="submit" class="Polaris-Button Polaris-Button--primary">
                    <span class="Polaris-Button__Content">
                      <span>Add Category</span>
                    </span>
                  </button>
                </div>
              </div>
            </div>
          </form>
        </div>
        <div class="Polaris-Card" v-if="CategoryBlocks.length > 0">
          <form @submit.prevent="addBlock">
            <div class="Polaris-Card__Header">
              <h2 class="Polaris-Heading">Schema Block Generator</h2>
            </div>
            <div class="Polaris-Card__Section">
              <div class="Polaris-FormLayout">
                <div class="Polaris-FormLayout__Item">
                  <div class="Polaris-Labelled__LabelWrapper">
                    <div class="Polaris-Label">
                      <label id="InputLabelLabel" for="InputLabel" class="Polaris-Label__Text">Label</label>
                    </div>
                  </div>
                  <div class="Polaris-TextField">
                    <input id="InputLabel" class="Polaris-TextField__Input" aria-label="Label" aria-labelledby="InputLabelLabel" aria-invalid="false" v-model="blockName">
                    <div class="Polaris-TextField__Backdrop"></div>
                  </div>
                </div>
                <div class="Polaris-FormLayout__Item">
                  <div class="Polaris-Labelled__LabelWrapper">
                    <div class="Polaris-Label">
                      <label id="InputIdLabel" for="InputId" class="Polaris-Label__Text">Setting ID</label>
                    </div>
                  </div>
                  <div class="Polaris-TextField">
                    <input id="InputId" class="Polaris-TextField__Input" aria-label="Setting ID" aria-labelledby="InputIdLabel" aria-invalid="false" placeholder="site_header_logo" v-model="blockId">
                    <div class="Polaris-TextField__Backdrop"></div>
                  </div>
                  <div class="Polaris-Labelled__HelpText" id="TextField3HelpText">No spaces or symbols. Separate words with underscores.</div>
                </div>
                <div class="Polaris-FormLayout__Item">
                  <div class="Polaris-Labelled__LabelWrapper">
                    <div class="Polaris-Label">
                      <label id="InputTypeLabel" for="InputType" class="Polaris-Label__Text">Input Type</label>
                    </div>
                  </div>
                  <div class="Polaris-Select">
                    <select id="InputType" class="Polaris-Select__Input" aria-invalid="false" v-model="inputType">
                    <option v-for="(inputType, index) in inputTypes" :key="index" :value="inputType" selected>{{ inputType }}</option>
                  </select>
                    <div class="Polaris-Select__Content" aria-hidden="true">
                      <span class="Polaris-Select__SelectedOption">{{ inputType }}</span>
                      <span class="Polaris-Select__Icon">
                        <span class="Polaris-Icon">
                          <svg class="Polaris-Icon__Svg" viewBox="0 0 20 20" focusable="false" aria-hidden="true"><path d="M13 8l-3-3-3 3h6zm-.1 4L10 14.9 7.1 12h5.8z" fill-rule="evenodd"></path></svg>
                        </span>
                      </span>
                    </div>
                    <div class="Polaris-Select__Backdrop"></div>
                  </div>
                </div>
                <div class="Polaris-FormLayout__Item">
                  <div class="Polaris-Labelled__LabelWrapper">
                    <div class="Polaris-Label">
                      <label id="InputDefaultLabel" for="InputDefault" class="Polaris-Label__Text">Default</label>
                    </div>
                  </div>
                  <div class="Polaris-TextField">
                    <input id="InputDefault" class="Polaris-TextField__Input" aria-label="Default" aria-labelledby="InputDefaultLabel" aria-invalid="false" v-model="inputDefault">
                    <div class="Polaris-TextField__Backdrop"></div>
                  </div>
                  <div class="Polaris-Labelled__HelpText" id="TextField3HelpText">Optional. Shows a default value if nothing has previously been set.</div>
                </div>
                <div class="Polaris-FormLayout__Item">
                  <div class="Polaris-Labelled__LabelWrapper">
                    <div class="Polaris-Label">
                      <label id="InputPlaceholderLabel" for="InputPlaceholder" class="Polaris-Label__Text">Placeholder</label>
                    </div>
                  </div>
                  <div class="Polaris-TextField">
                    <input id="InputPlaceholder" class="Polaris-TextField__Input" aria-label="Placeholder" aria-labelledby="InputPlaceholderLabel" aria-invalid="false" v-model="inputPlaceholder">
                    <div class="Polaris-TextField__Backdrop"></div>
                  </div>
                  <div class="Polaris-Labelled__HelpText" id="TextField3HelpText">Displays a placeholder inside of the field.</div>
                </div>
              </div>
            </div>
            <div class="Polaris-Card__Footer">
              <div class="Polaris-ButtonGroup">
                <div class="Polaris-ButtonGroup__Item">
                  <button type="submit" class="Polaris-Button Polaris-Button--primary">
                    <span class="Polaris-Button__Content">
                      <span>Add Block</span>
                    </span>
                  </button>
                </div>
              </div>
            </div>
          </form>
        </div>
      </div>
      <div class="Polaris-Layout__Section Polaris-Layout__Section--secondary">
        <div class="Polaris-Card">
          <div class="Polaris-Card__Header">
            <h2 class="Polaris-Heading">Result</h2>
          </div>
          <div class="Polaris-Card__Section">
            <p>This shows the result of the schema blocks.</p>
          </div>
          </div>
          <div class="Polaris-Card" v-if="CategoryBlocks.length > 0">
          <draggable v-model="CategoryBlocks" @start="drag=true" @end="drag=false">
            <div class="Polaris-Card__Section" v-for="(data, index) in CategoryBlocks" :key="index">
                <div class="Polaris-Card__Header">
                  <div class="Polaris-Stack Polaris-Stack--alignmentBaseline">
                    <div class="Polaris-Stack__Item Polaris-Stack__Item--fill">
                      <h2 class="Polaris-Heading">{{ data.catName }}</h2>
                    </div>
                  </div>
                </div>
                <div class="Polaris-Card__Section">
                  <p>Add variants if this product comes in multiple versions, like different sizes or colors.</p>
                </div>
            </div>
          </draggable>
          </div>
          <div class="Polaris-Card" v-if="SchemaBlocks.length > 0">
          <draggable v-model="SchemaBlocks" :options="{handle: '.Drag-Button', group:'people', move: true}" @start="drag=true" @end="drag=false">
          <transition-group>
            <div class="Polaris-Card__Section" v-for="(data, index) in SchemaBlocks" :key="index">
              <div class="Polaris-Stack Polaris-Stack--alignmentBaseline">
              <div class="Polaris-Stack__Item Polaris-Stack__Item--fill">
                <h2 class="Polaris-Heading">Name: {{ data.blockName }}</h2>
              </div>
              <div class="Polaris-Stack__Item" v-if="SchemaBlocks.length > 1">
                <div class="Polaris-Stack__Item">

                <div class="Polaris-ButtonGroup">
                  <div class="Polaris-ButtonGroup__Item"><button type="button" class="Polaris-Button Polaris-Button--destructive"><span class="Polaris-Button__Content"><span>Add variant</span></span></button></div>
                  <div class="Polaris-ButtonGroup__Item Polaris-ButtonGroup__Item--plain">
                    <button type="button" class="Drag-Button Polaris-Button Polaris-Button--plain">
                      <span class="Polaris-Button__Content">
                        <span class="Polaris-Icon">
                        <svg class="Polaris-Icon__Svg" width="4" height="16" viewBox="0 0 4 16" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><defs><path d="M10 6c-1.103 0-2-.897-2-2s.897-2 2-2 2 .897 2 2-.897 2-2 2zm0 2c1.103 0 2 .897 2 2s-.897 2-2 2-2-.897-2-2 .897-2 2-2zm0 6c1.103 0 2 .897 2 2s-.897 2-2 2-2-.897-2-2 .897-2 2-2z" id="a"/></defs><g transform="translate(-8 -2)" fill="none" fill-rule="evenodd"><mask id="b" fill="#fff"><use xlink:href="#a"/></mask><use fill="#31373D" xlink:href="#a"/></g></svg>
                      </span></span>
                    </button></div>
                </div>
                </div>
              </div>
            </div>

              <p><strong class="Polaris-TextStyle--variationStrong">Setting ID:</strong> {{ data.blockId }}</p>
              <p><strong class="Polaris-TextStyle--variationStrong">Input Type:</strong> {{ data.inputType }}</p>
              <p><strong class="Polaris-TextStyle--variationStrong">Default:</strong> {{ data.inputDefault }}</p>
              <p><strong class="Polaris-TextStyle--variationStrong">Placeholder:</strong> {{ data.inputPlaceholder }}</p>
            </div>
          </transition-group>
          </draggable>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
export default {

  name: 'SchemaBuilder',
  data() {
    return {
      SchemaBlocks: [],
      CategoryBlocks: [],
      blockName: '',
      blockId: '',
      inputDefault: '',
      inputPlaceholder: '',
      block: '',
      blocks: [],
      inputType: 'Text',
      inputTypes: [
        "Text",
        "Text Area",
        "Rich Text",
        "Range",
        "Number",
        "Image Picker",
        "Radio",
        "Checkbox",
      ],
      catName: ''
    }
  },
  methods: {
    addBlock() {
      this.SchemaBlocks.push({
        blockName: this.blockName,
        blockId: this.blockId,
        inputType: this.inputType,
        inputPlaceholder: this.inputPlaceholder,
        inputDefault: this.inputDefault
      })
      this.inputType = 'Text';
      this.blockName = '';
      this.blockId = '';
      this.inputPlaceholder = '';
      this.inputDefault = '';

    },
    addCategory() {
      this.CategoryBlocks.push({
        catName: this.catName
      })
      this.catName = '';
    }
  },
  components: {
    draggable
  }
}
</script>

<style>
  .container {
    width: 100%;
    max-width: 960px;
    margin: 0 auto;
  }
  .button-group {
    margin-top: 35px;
  }
</style>
