<template>
  <div>
    <button type="button" class="open-btn" @click="isOpen = true">Open Modal</button>
    <dialog class="dialog" 
    ref="dialogRef" :open="isOpen" role="dialog" aria-labelledby="dialog1_label" aria-modal="true" @keydown.esc="isOpen = false" @keydown.tab="handleTab"
      tabindex="0">
      <div class="dialog-container">
 
      <h1 id="dialog1_label" class="dialog_label">{{ title }}</h1>
      <slot></slot>
      <button type="button" class="close-btn" @click="() => { console.log('cancel clicked'); isOpen = false }">Cancel</button>
      </div>
    </dialog>
  </div>
</template>


<script setup>
import { ref, watch, nextTick } from 'vue';
const isOpen = ref(false);
const dialogRef = ref(null);
const firstElement = ref(null)
const lastElement = ref(null)
const triggerElement = ref(null)

defineProps({
  title: {
    type: String,
    required: true
  }
})
const handleTab = (event) =>{
  if (event.shiftKey) {
    if (document.activeElement === firstElement.value) {
      lastElement.value.focus()
      event.preventDefault()
    }
  }
  else if (document.activeElement === lastElement.value) {
    firstElement.value.focus()
    event.preventDefault()
  }
}
watch(isOpen, (newValue) => {
  if (newValue) {
    const focusableElements = dialogRef.value.querySelectorAll(
      'button, input, select, textarea, a[href]'
    )
    triggerElement.value = document.activeElement
    firstElement.value = focusableElements[0]
    lastElement.value = focusableElements[focusableElements.length - 1]
    nextTick(() => {
      dialogRef.value.focus()
    })
 
  } else {
    triggerElement.value.focus()
  }
  })

</script>


<style scoped>
:deep(.dialog_form) {
  display: flex;
  flex-direction: column;
  gap: var(--space-sm);
  align-items: flex-start;
  margin-bottom: var(--space-lg);
}
:deep(.btn-submit) {

}
</style>