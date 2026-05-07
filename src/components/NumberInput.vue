<template>
  <input type="number" :value="number" @input="onInput" />
</template>

<script>
export default {
  name: "NumberInput",

  props: {
    number: Number,
    numberModifiers: Object,
  },

  emits: ["update:number"],

  methods: {
    onInput(e) {
      let val = e.target.value;

      if (val === "") {
        this.$emit("update:number", "");
        return;
      }

      val = Number(val);

      if (this.numberModifiers?.even && val % 2 !== 0) {
        return;
      }

      this.$emit("update:number", val);
    },
  },
};
</script>
