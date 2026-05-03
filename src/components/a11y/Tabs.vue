<template>
  <div id="main-tablist" class="main-tablist" role="tablist">
    <button v-for="(tab, index) in props.tabs" :key="index" :id="`tab-${index}`" role="tab"
      :aria-controls="`panel-${index}`" class="button-tab">
      {{ tab.title }}
    </button>
  </div>
  <div v-for="(panel, index) in props.tabs" :key="index" :id="`panel-${index}`" role="tabpanel"
    :aria-labelledby="`tab-${index}`" class="container-tabpanel">
    {{ panel.content }}
  </div>
</template>


<script setup>
const props = defineProps({
  tabs: {
    type: Array,
    default: () => [
      { title: 'Commedy Movie', content: 'The best commedy movie is' },
      { title: 'Sci-Fi Movie', content: 'The best sci-fi movie is' },
      { title: 'Horror Movie', content: 'The best horror movie is' }
    ]
  }
})
</script>


<style scoped></style>