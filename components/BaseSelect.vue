<template>
  <div :class="['input-group',{ 'icon-valid': valid }, { 'icon-error': error }]" >
    <select 
      :name="name" 
      :value="localValue" 
      v-bind="$attrs" 
      :class="['select-input', { valid }, { error }]"
      @input="handleInput"  
    >
      <option 
        v-for="(option, index) in options" 
        :key="index" 
        :value="option.value">
        {{ option.text }}
      </option>
    </select>

    <transition name="error-message">
      <span
        v-if="errorMessage"
        class="error-message"
      >
        {{ errorMessage }}
      </span>
    </transition>
  </div>
</template>

<script>
import lodash from 'lodash';

export default {
  name: 'BaseSelect',
  inheritAttrs: false,
  props: {
    debounceTime: {
      type: Number,
      default: 0,
    },
    error: {
      type: Boolean,
      default: false,
    },
    errorMessage: {
      type: String,
      default: '',
    },
    mask: {
      type: Function,
      default: value => value,
    },
    parse: {
      type: Function,
      default: value => value,
    },
    valid: {
      type: Boolean,
      default: false,
    },
    value: {
      type: String,
      default: null,
    },
    stringMask:{
      type: String,
      default: ''
    },
    type:{
      type: String,
      default: 'text'
    },
    name:{
      type: String,
      default: ''
    },
    options:{
      type: Array,
      default: []
    }
  },
  data() {
    return {
      localValue: null,      
    };
  },
  computed: {
    handleInput() {
      return lodash.debounce((event) => {
        this.$emit('input', this.parse(event.target.value));
      }, this.debounceTime);
    },
  },
  watch: {
    value(newValue) {
      this.localValue = this.mask(newValue);
    },
  },
};
</script>

<style lang="scss" scoped>
  @import "../assets/css/paleta";
  @import "../assets/css/speed";


.input-group{
  position: relative;
}
.icon-valid:after{
  content: "\E876";
  display: block;
  position: absolute;
  font-family: "Material Icons"; 
  color: $green-accent;
  font-size: 24px;
  top: 7px;
  right: 15px;      
}

.icon-error:after{
  content: "\E001";
  position: absolute;
  font-family: "Material Icons";
  color: #E34C4C;
  font-size: 24px;
  top: 7px;
  right: 15px;       
}

.select-input {
  border: 1px solid $medium-neutral;
  background: $white;
  border-radius: 4px;
  height: 40px;
  width: 100%;
  outline: none;
  padding: 8px 16px;
  color: $dark-neutral;
  font-size: 16px;
  font-weight: 400;
  line-height: 1.5em;
  transition: background-color .2s, border-color .2s, color .2s;
  position: absolute;
  font-family: 'Lato', sans-serif !important;

  &:focus {
    border-color: $light-dark-blue;
  }
  &:disabled {
    background-color: $light-neutral;
    border-color: $medium-neutral;
    pointer-events: none;
  }
  &::placeholder {
    color: $medium-neutral;
  }
}

.valid {
  padding-right: 48px;
  border-color: $green-accent !important;
}

.error {
  border-color: $red-accent !important;
}

.error-message {
  font-size: 12px;
  font-weight: 400;
  line-height: 2em;
  float: left;
  color: $red-accent;
}

.error-message-enter-active, .error-message-leave-active {
  transition: transform 0.2s $decelerate-easing, opacity 0.1s $decelerate-easing;
}
.error-message-enter, .error-message-leave-to {
  transform: translate(0, -100%);
  opacity: 0;
  transition: transform .2s $accelerate-easing, opacity 0.1s $accelerate-easing;
}

.error-input-indication, .valid-input-indication  {
  float: right;
  position: absolute;
  margin-top: 8px;
  right: 40px;
}

.error-input-indication {
  color: $red-accent;
}

.valid-input-indication {
  color: $green-accent;
}
</style>