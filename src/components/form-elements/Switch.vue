<template>
  <div class="form-group switch-group">
    <label v-if="label" class="control-label" :class="labelColumnClass">{{ label }}:</label>
    <div :class="inputColumnClass">
      <label class="switch-component">
        <input type="checkbox"
          :id="id"
          :name="name"
          :checked="checked"
          v-on:change="updateValue($event.target.checked)">
        <div class="slider round">
          <span v-if="labels" class="yes-label">Yes</span>
          <span v-if="labels" class="no-label">No</span>
        </div>
      </label>
      <p v-if="helper" class="help-block">{{ helper }}</p>
    </div>
  </div>
</template>

<script>
  export default {
    model: {
      prop: 'checked',
      event: 'change'
    },
    props: {
      id: String,
      name: {
        type: String,
        required: true
      },
      label: {
        type: String
      },
      labels: {
        type: Boolean,
        default: false
      },
      helper: String,
      stacked: {
        type: Boolean,
        default: false
      },
      checked: Boolean,
      labelColumn: {
        type: String,
        default: 'col-sm-2'
      },
      inputColumn: {
        type: String,
        default: 'col-sm-10'
      }
    },
    computed: {
      labelColumnClass() {
        if (!this.stacked) {
          return this.labelColumn
        }
      },
      inputColumnClass() {
        if (!this.stacked && this.label) {
          return this.inputColumn
        }
      }
    },
    methods: {
      updateValue(value) {
        this.$emit('change', value)
      }
    }
  };
</script>

<style>
  /* The switch */
  .switch-component {
    position: relative;
    display: inline-block;
    width: 60px;
    height: 34px;
  }
  .switch-component input {
    display: none;
  }

  /* The slider */
  .slider {
    position: absolute;
    cursor: pointer;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: #ccc;
    -webkit-transition: .4s;
    transition: .4s;
  }
  .slider:before {
    position: absolute;
    content: "";
    height: 26px;
    width: 26px;
    left: 4px;
    bottom: 4px;
    background-color: white;
    -webkit-transition: .4s;
    transition: .4s;
  }
  input:checked + .slider {
    background-color: #428bca;
  }
  input:focus + .slider {
    box-shadow: 0 0 1px #428bca;
  }
  input:checked + .slider:before {
    -webkit-transform: translateX(26px);
    -ms-transform: translateX(26px);
    transform: translateX(26px);
  }

  /* Rounded sliders */
  .slider.round {
    border-radius: 34px;
    display: flex;
    align-items: center;
    font-size: 11px;
    justify-content: space-between;
  }
  .slider.round:before {
    border-radius: 50%;
  }
  .slider.round .yes-label {
    padding-left: 5px;
    color: #FFF;
    text-transform: uppercase;
  }
  .slider.round .no-label {
    padding-right: 7px;
    text-transform: uppercase;
  }
</style>
