<script setup>
import {onClickOutside} from '@vueuse/core'

const props = defineProps({
  isOpen: Boolean,
});

const emit = defineEmits(["modal-close"]);

const target = ref(null)
onClickOutside(target, ()=>emit('modal-close'))

</script>

<template>
  <div v-if="isOpen" class="modal-mask">
    <div class="modal-wrapper">
      <div class="modal-container" ref="target">
        <div class="modal-body">
          <slot/>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal-mask {
  position: absolute;
  z-index: 9998;
  top: 40px;
  left: -530px;
  width: 100%;
  height: 100%;
}
.modal-container {
  width: 800px;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
}

</style>