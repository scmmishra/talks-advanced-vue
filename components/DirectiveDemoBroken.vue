<template>
  <div class="text-xs p-3 flex-grow">
    <div class="space-y-1">
      <button @click="toggle" class="button bg-green-500 hover:bg-green-600">
        Menu
      </button>
      <div
        v-if="isOpen"
        class="
          w-48
          bg-gray-100
          rounded-md
          divide-y divide-gray-100
          overflow-hidden
        "
      >
        <div class="px-2 py-1 hover:bg-gray-200 font-semibold cursor-pointer">
          Home
        </div>
        <div class="px-2 py-1 hover:bg-gray-200 font-semibold cursor-pointer">
          Settings
        </div>
        <div class="px-2 py-1 hover:bg-gray-200 font-semibold cursor-pointer">
          Support
        </div>
        <div class="px-2 py-1 hover:bg-gray-200 font-semibold cursor-pointer">
          Logout
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isOpen: false,
    };
  },
  methods: {
    toggle() {
      this.isOpen = !this.isOpen;
    },
    close() {
      this.isOpen = false;
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
