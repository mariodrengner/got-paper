<template>
  <div class="uiOutput form-group row" :class="classes">
    <label class="uiOutput__label col-6 col-md-8 col-form-label">{{ label }}</label>
    <span class="uiOutput__slot col-6 col-md-4">
      <slot>
        <output class="uiOutput__value">{{ output }}</output>
      </slot>
    </span>
  </div>
</template>

<script>
export default {
  props: {
    label: String,
    value: Number,
    precision: {
      type: Number,
      default: 0
    }
  },

  computed: {
    output () {
      return (this.value || 0).toFixed(this.precision)
    },

    model: {
      get () {
        return this.value
      },
      set (value) {
        this.$emit('input', value)
      }
    },

    classes () {
      return this.$slots.default ? '' : 'hasSlot'
    }
  }
}
</script>

<style lang="scss">
.uiOutput {
  &__label,
  &__slot,
  &__value {
    vertical-align: middle;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  &__slot {
    align-items: flex-end;
  }

  &__label {
    // font-weight: bold;
  }

  &__value {
    font-size: 2em;
    font-weight: 700;
    display: block;
    vertical-align: center;
  }

  &.hasSlot &__value {
    padding-right: 36px;
    text-align: right;
    vertical-align: center;
  }
}
</style>
