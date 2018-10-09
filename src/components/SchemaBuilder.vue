<template>
  <div class="container">
    <polaris-layout>
      <polaris-layout-section secondary>
        <polaris-card title="Create New Category" :primary-footer-action="{content: 'Add Category', onAction: addCategory}" sectioned>
          <polaris-form-layout>
            <polaris-text-field v-model="catName"
                label="Category Name">
            </polaris-text-field>
          </polaris-form-layout>
        </polaris-card>
        <polaris-card title="Schema Block Generator" v-if="CategoryBlocks.length > 0" :primary-footer-action="{content: 'Add Block', onAction: addBlock}">
          <polaris-card-section>
            <polaris-form-layout>
              <polaris-text-field v-model="blockName"
                  label="Label">
              </polaris-text-field>
              <polaris-text-field v-model="blockId" help-text="No spaces or symbols. Separate words with underscores."
                  label="Setting ID" placeholder="site_header_logo">
              </polaris-text-field>


              <polaris-select
                  v-model="inputType"
                  label="Input Type"
                  :options="[
                      'Text',
                      'Text Area',
                      'Rich Text',
                      'Range',
                      'Number',
                      'Image Picker',
                      'Radio',
                      'Checkbox',
                      'Select'
                  ]"
                  placeholder="Input Type">
              </polaris-select>
              <!-- <div class="Polaris-FormLayout__Item">
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
              </div> -->
              <polaris-form-layout-group v-if="inputType === 'Select'" condensed>
                <polaris-text-field
                  label="Option Label">
                </polaris-text-field>
                <polaris-text-field
                  label="Option Value">
                </polaris-text-field>
              </polaris-form-layout-group>
              <polaris-text-field label="Default" v-model="inputDefault">

              </polaris-text-field>
              <polaris-text-field label="Placeholder" v-model="inputPlaceholder">

              </polaris-text-field>
            </polaris-form-layout>
          </polaris-card-section>
        </polaris-card>
      </polaris-layout-section>
      <polaris-layout-section secondary>
        <polaris-card title="Result" sectioned>
          <p>This shows the result of the schema blocks.</p>
        </polaris-card>
        <polaris-card title="Categories">
          <draggable @start="drag=true" @end="drag=false">
            <polaris-card-section :title="data.catName" v-model="CategoryBlocks" v-for="(data, index) in CategoryBlocks" :key="index" v-if="CategoryBlocks.length > 0">
              <p>Add variants if this product comes in multiple versions, like different sizes or colors.</p>
            </polaris-card-section>
          </draggable>
        </polaris-card>
          <polaris-card v-if="SchemaBlocks.length > 0">
          <draggable v-model="SchemaBlocks" :options="{handle: '.Drag-Button', group:'Color', move: true}" @start="drag=true" @end="drag=false">
            <polaris-card-section :title="data.blockName" v-for="(data, index) in SchemaBlocks" :key="index">

              <!-- <div class="Polaris-Stack Polaris-Stack--alignmentBaseline">
                <div class="Polaris-Stack__Item" v-if="SchemaBlocks.length > 1">
                  <div class="Polaris-Stack__Item">
                  <div class="Polaris-ButtonGroup">
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
              </div> -->
              <div>
                <polaris-text-style><polaris-text-style variation="strong">Setting ID:</polaris-text-style> {{ data.blockId }}</polaris-text-style>
              </div>
              <div>
                <polaris-text-style><polaris-text-style variation="strong">Input Type:</polaris-text-style> {{ data.inputType }}</polaris-text-style>
              </div>
              <div>
                <polaris-text-style><polaris-text-style variation="strong">Default:</polaris-text-style> {{ data.inputDefault }}</polaris-text-style>
              </div>
              <div>
                <polaris-text-style><polaris-text-style variation="strong">Placeholder:</polaris-text-style> {{ data.inputPlaceholder }}</polaris-text-style>
              </div>
            </polaris-card-section>
          </draggable>
        </polaris-card>
      </polaris-layout-section>
    </polaris-layout>
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
        "Select"
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
    },
    // addRow: function () {
    //   var elem = document.createElement('tr');
    //   this.rows.push({
    //     title: "",
    //     description: "",
    //     file: {
    //       name: 'Choose File'
    //     }
    //   });
    // },
  },
  components: {
    draggable
  }
}
</script>

<style lang="scss">

  .container {
    width: 100%;
    max-width: 960px;
    margin: 0 auto;
  }
  .button-group {
    margin-top: 35px;
  }
</style>
