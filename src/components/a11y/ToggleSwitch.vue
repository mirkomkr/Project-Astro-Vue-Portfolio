<template>
  <div>
    <span id="switch-label">{{ props.label }}</span>
    <button @click="isChecked = !isChecked" role="switch" :aria-checked="isChecked.toString()"
      aria-labelledby="switch-label">
      <span class="track" :class="{ 'is-active': isChecked }">
        <span class="thumb"></span>
      </span>
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const props = defineProps({
  label: {
    type: String,
    default: 'Event Switch'
  },
  checked: {
    type: Boolean,
    default: false
  }
})
const isChecked = ref(props.checked)
</script>
<style scoped>
#switch-label{
  display: flex;
  flex-direction: column;
  margin-bottom: 1.5rem;
}

button {
  background: none;
  border: none;
  padding: 0;
  cursor: pointer;
}

.track {
  position: relative;
  display: inline-block;
  background-color: var(--border-main);
  border-radius: var(--border-radius-large);
  width: 4rem;
  height: 2rem;
}

.thumb {
  position: absolute;
  cursor: pointer;
  background-color: var(--switch-active);
  width: 1.5rem;
  height: 1.5rem;
  border-radius: var(--border-radius-large);
  top: 50%;
  transform: translateY(-50%);
  left: 0.25rem;
  -webkit-transition: .4s;
  transition: .4s;
}


.is-active .thumb {
  transform: translateX(1.75rem) translateY(-50%);
  background-color: var(--border-main);
}

.is-active.track{
  background-color: var(--switch-active);
}
</style>