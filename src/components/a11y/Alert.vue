<template>
  <div class="messageAlert" :class="`messageAlert--${props.type}`" :role="props.type === 'error' ? 'alert' : 'status'">
    <span aria-hidden="true">
      <svg v-if="props.type === 'error'" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
        stroke-width="1.5" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round"
          d="m9.75 9.75 4.5 4.5m0-4.5-4.5 4.5M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
      </svg>
      <svg v-else-if="props.type === 'warning'" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
        stroke-width="1.5" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round"
          d="M12 9v3.75m-9.303 3.376c-.866 1.5.217 3.374 1.948 3.374h14.71c1.73 0 2.813-1.874 1.948-3.374L13.949 3.378c-.866-1.5-3.032-1.5-3.898 0L2.697 16.126ZM12 15.75h.007v.008H12v-.008Z" />
      </svg>
      <svg v-else-if="props.type === 'info'" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
        stroke-width="1.5" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round"
          d="M12 9v3.75m9-.75a9 9 0 1 1-18 0 9 9 0 0 1 18 0Zm-9 3.75h.008v.008H12v-.008Z" />
      </svg>
      <svg v-else xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
        stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round"
          d="M9 12.75 11.25 15 15 9.75M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
      </svg>
    </span>
    <p><strong>{{ labels[props.type] }}</strong> {{ props.message }}</p>
  </div>
</template>

<script setup>
const labels = {
  error: 'Error',
  warning: 'Warning',
  success: 'Success',
  info: 'Info'
}
const props = defineProps({
  type: {
    type: String,
    default: 'info'
  },
  message: {
    type: String,
    default: ''
  }
})
</script>
<style scoped>
.messageAlert {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: var(--space-md);
  position: static;
  margin-bottom: 1.5rem;
}

.messageAlert--error {
  color: var(--alert-error-text);
  background-color: var(--alert-error-bg);
  border: 0.1rem solid var(--alert-error-border);
  border-radius: var(--border-radius-small);
  width: fit-content;
  padding: 0.3rem;
}

.messageAlert--warning {
  color: var(--alert-warning-text);
  background-color: var(--alert-warning-bg);
  border: 0.1rem solid var(--alert-warning-border);
  border-radius: var(--border-radius-small);
  width: fit-content;
  padding: 0.3rem;
}

.messageAlert--info {
  color: var(--alert-info-text);
  background-color: var(--alert-info-bg);
  border: 0.1rem solid var(--alert-info-border);
  border-radius: var(--border-radius-small);
  width: fit-content;
  padding: 0.3rem;
}

.messageAlert--success {
  color: var(--alert-success-text);
  background-color: var(--alert-success-bg);
  border: 0.1rem solid var(--alert-success-border);
  border-radius: var(--border-radius-small);
  width: fit-content;
  padding: 0.3rem;
}

p{
  color: var(--text-main);
}
svg {
  width: 1.5rem;
  height: 1.5rem;
  flex-shrink: 0;
}
</style>