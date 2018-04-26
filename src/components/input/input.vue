<template>
  <div
    :class="[
      type === 'textarea' ? 'kcp-textarea' : 'kcp-input',
      inputSize ? 'kcp-input--' + inputSize : '',
      {
        'isDisabled': inputDisabled,
        'el-input-group': $slots.prepend || $slots.append,
        'el-input-group--append': $slots.append,
        'el-input-group--prepend': $slots.prepend
      }
    ]"
  >
    <template v-if="type !== 'textarea'">
      <!-- 前置元素，slot-->
      <div class="kcp-input-group__prepend" v-if="$slots.prepend">
        <slot name="prepend"></slot>
      </div>
      <input
        class="kcp-input-inner"
        :type="type"
        :disabled="inputDisabled"
        :value="currentValue"
        ref="input"
        v-bind="$attrs"
        @input="handleInput"
        @focus="handleFocus"
        @blur="handleBlur"
        @change="handleChange"
      >
      <!-- 后置元素，slot -->
      <div class="kcp-input-group__append" v-if="$slots.append">
        <slot name="append"></slot>
      </div>
    </template>
    <textarea
      v-else
      :disabled="inputDisabled"
      :value="currentValue"
      ref="textarea"
      v-bind="$attrs"
      @input="handleInput"
      @focus="handleFocus"
      @blur="handleBlur"
      @change="handleChange"
    >
    </textarea>
  </div>
</template>

<script>
/** input支持的属性和事件
 * @argument {{ Boolean }} disabled 是否禁止输入，true为禁止，默认false
 * @argument {{ String }} type 输入框的类型，值为text或textarea，默认text
 * @argument {{ String }} size 输入框尺寸，medium 正常/ small 小/ mini 最小，只在 type!="textarea" 时有效
 * @argument {{ Slot }} prepend 输入框前置元素
 * @argument {{ Slot }} append 输入框后置元素
 * @event input 输入事件
 * @event focus 获取焦点事件
 * @event blur 失去焦点事件
 * @event change 失去焦点后，文本内容发生变化时触发
 */

/** 针对Slot的例子
 * <template slot="prepend">prepend</template>
 */
export default {
  name: 'kcpInput',

  componentName: 'kcpInput',

  data () {
    return {
      currentValue: this.value === undefined ? '' : this.value
    }
  },
  props: {
    type: {
      type: String,
      default: 'text'
    },
    disabled: Boolean,
    size: String,
    value: [String, Number]
  },
  computed: {
    inputSize () {
      return this.size
    },
    inputDisabled () {
      return this.disabled
    }
  },
  methods: {
    setCurrentValue (value) {
      this.currentValue = value
    },
    handleInput (event) {
      const value = event.target.value
      this.$emit('input', value)
    },
    handleFocus (event) {
      this.$emit('focus', event)
    },
    handleBlur (event) {
      this.$emit('blur', event)
    },
    handleChange (event) {
      this.$emit('change', event.target.value)
    }
  },
  watch: {
    'value' (value, oldValue) {
      this.setCurrentValue(value)
    }
  },
  mounted () {

  }
}
</script>
