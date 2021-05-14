<template>
  <div class="text-xs code-demo p-3 flex-grow">
    <div class="flex items-center space-x-2 justify-center p-4">
      <button @click="setOn()" class="button bg-green-500 hover:bg-green-600">
        Toggle On
      </button>
      <button @click="setOff()" class="button bg-red-500 hover:bg-red-600">
        Toggle Off
      </button>
    </div>
    <div class="text-center">
      <span v-if="on" class="text-green-600">It's <b>On.</b></span>
      <span v-else class="text-red-600">It's <b>Off.</b></span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      on: false,
    };
  },
  methods: {
    setOn() {
      this.on = true;
    },
    setOff() {
      this.on = false;
    },
  },
};
</script>

<style>
.button {
  padding: 4px 12px;
  color: white;
  border-radius: 4px;
}
</style>
