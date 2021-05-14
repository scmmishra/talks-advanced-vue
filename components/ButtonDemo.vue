<template>
  <div class="code-demo py-12 flex space-y-4 justify-center">
    <button @click="countEmit" class="button hover:bg-green-40">Button</button>
  </div>
  <div class="text-xs code-demo p-3 flex-grow h-72">
    <div class="flex items-center justify-between">
      <h5 class="uppercase font-bold text-xs">Event Log</h5>
      <div class="space-x-2">
        <span
          >Click event emitted <b>{{ this.count }}</b> times</span
        >
        <button
          @click="reset"
          class="px-2 py-1 text-xs bg-gray-200 hover:bg-gray-300 rounded"
        >
          Reset
        </button>
      </div>
    </div>
    <div class="space-y-2 mt-3 h-60 overflow-scroll">
      <div
        v-for="(event, index) in events.reverse()"
        class="text-xs bg-gray-100 hover:bg-blue-100 p-2 rounded-md"
        :key="index"
      >
        <span
          class="text-xs font-mono text-pink-400 font-bold"
          style="font-size: 0.65rem"
          >`click`</span
        >
        event emitted at
        <b>{{ event }}</b>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      count: 0,
      events: [],
    };
  },
  methods: {
    reset() {
      this.count = 0;
      this.events = [];
    },
    countEmit() {
      const options = {
        hour: "numeric",
        minute: "numeric",
        second: "numeric",
        fractionalSecondDigits: 3,
        hour12: true,
      };
      const date = new Date();
      this.events.push(new Intl.DateTimeFormat("en-US", options).format(date));
      this.count = this.count + 1;
    },
  },
};
</script>

<style>
.button {
  padding: 4px 12px;
  color: white;
  border-radius: 4px;
  background-color: #22c55e;
}
</style>
