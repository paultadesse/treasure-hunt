<template lang="">
  <teleport to="body">
    <div
      ref="modal-backdrop"
      class="fixed z-10 inset-0 overflow-y-auto bg-black bg-opacity-50"
      v-show="show"
    >
      <div
        class="flex items-start justify-center min-h-screen pt-24 text-center"
      >
        <div
          class="bg-white rounded-lg text-left overflow-hidden shadow-xl p-8 w-1/2"
          role="dialog"
          ref="modal"
          aria-modal="true"
          aria-labelledby="modal-headline"
        >
          <slot>just fallback. . .</slot>
        </div>
      </div>
    </div>
  </teleport>
</template>
<script setup>
defineProps({
  show: {
    type: Boolean,
    default: false,
  },
});
</script>
<style lang=""></style>
