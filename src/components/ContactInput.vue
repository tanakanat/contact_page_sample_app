<template>
  <div class="mb-3">
    <label :for="id" class="form-label">{{ label }}</label>
    <span v-if="!!validationMessage" class="ml-2 text-danger rounded"
      >[!]{{ validationMessage }}</span
    >
    <input
      :type="type"
      class="form-control"
      :id="id"
      :placeholder="placeHolder"
      :value="value"
      @input="changevValue"
    />
  </div>
</template>

<script>
export default {
  name: "ContactInput",
  props: {
    id: {
      type: String,
      required: true,
    },
    type: {
      type: String,
      required: true,
    },
    label: {
      type: String,
      required: true,
    },
    value: {
      type: String,
      required: true,
    },
    placeHolder: {
      type: String,
      required: true,
    },
    validationMessage: {
      type: String,
      required: true,
    },
  },
  methods: {
    changevValue(ev) {
      this.$emit("changeValue", ev);
    },
  },
};
</script>