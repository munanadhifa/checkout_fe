<template>
  <div>
    <label for="label" class="block m-3 text-sm font-medium text-gray-700">{{
      label
    }}</label>
    <div class="mt-1">
      <input
        :type="type"
        id="inputVal"
        :value="inputVal"
        @input="$emit('update:inputVal', $event.target.value)"
        :required="isRequired"
        v-if="isTextArea"
        class="
          h-8
          p-3
          w-full
          rounded-md
          border-gray-300
          shadow-sm
          focus:border-indigo-500 focus:ring-indigo-500
          sm:text-sm
          drop-shadow-md
        "
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "CustomInput",
  props: {
    label: {
      type: String,
      default: "",
    },
    isRequired: {
      type: String,
      default: "true",
    },
    type: {
      type: String,
      default: "text",
    },
    inputVal: {
      type: String,
      default: "",
    },
  },
  methods: {
    isTextArea() {
      console.log(this.type);
      return this.type === "textArea" ? false : true;
    },
  },
  computed: {
    isRequired() {
      console.log(this.isRequired);
      return this.isRequired === "true" ? true : false;
    },
  },
};
</script>