<template>
  <input
    type="text"
    :value="modelValue"
    @input="onInput"
    placeholder="Пишіть тут..."
    style="border: 1px solid black; padding: 5px; margin: 0 10px;"
  />
</template>

<script>
export default {
  props: ['modelValue', 'modelModifiers'],
  emits: ['update:modelValue'],
  methods: {
    onInput(e) {
      let val = e.target.value;
      if (this.modelModifiers?.capitalize && val) {
        val = val.charAt(0).toUpperCase() + val.slice(1);
      }
      this.$emit('update:modelValue', val);
    }
  }
}
</script>