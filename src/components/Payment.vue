<template>
  <dl class="mt-5 grid grid-cols-1 gap-5 ml-10" @click="setValue()">
    <div class="overflow-hidden rounded-lg bg-white px-4 py-5 shadow sm:p-6">
      <dt class="truncate text-sm font-medium text-gray-500">
        {{ name }}
      </dt>
      <dd class="mt-1 text-3xl font-semibold tracking-tight text-gray-900">
        {{ price }}
      </dd>
    </div>
  </dl>
</template>

<script >
import { formatPrice } from "../main";

export default {
  props: {
    name: String,
    price: Number,
  },
  methods: {
    setValue() {
      this.$emit("payment", "pay");
    },
  },
  watch: {
    price() {
      return formatPrice(this.price);
    },
  },
};
</script>