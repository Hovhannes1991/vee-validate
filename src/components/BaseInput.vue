<template>
  <div class="base-input">
    <label
      >{{ label }}
      <input :type="type" :name="name" @input="onInput" @change="onChange" />
      <p class="error-message" v-if="error">{{ error }}</p>
    </label>
  </div>
</template>

<script>
export default {
  name: "BaseInput",
  props: {
    modelvalue: {},
    type: { String, default: "text" },
    name: { String, default: "" },
    label: { String, default: "" },
    lazy: { Boolean, default: false },
    error: { String },
  },

  methods: {
    onInput(e) {
      if (this.lazy) return;
      this.$emit("update:modelValue", e.target.value);
    },

    onChange(e) {
      if (!this.lazy) return;
      this.$emit("update:modelValue", e.target.value);
    },
  },
};
</script>

<style>
.base-input input {
  position: relative;
  width: 100%;
  height: 50px;
  border: 2px solid green;
  outline: none;
}

.base-input .error-message {
  position: absolute;
  color: darkred;
}
</style>
