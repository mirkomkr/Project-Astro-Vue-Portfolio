<template>
  <div class="tab-container">
    <h1>Tabs</h1>
  <div id="main-tablist" class="main-tablist" role="tablist" @keydown.right="activeTab === props.tabs.length - 1 ? activeTab = 0 : activeTab++" @keydown.left="activeTab === 0 ? activeTab = props.tabs.length - 1 : activeTab--">
    <button :ref="el => tabRefs[index] = el" @click="activeTab = index" :aria-selected="index === activeTab ? true : false" v-for="(tab, index) in props.tabs" :key="index" :id="`tab-${index}`" role="tab"
      :aria-controls="`panel-${index}`" class="button-tab">
      {{ tab.title }}
    </button>
  </div>
  <div v-show="activeTab === index" v-for="(panel, index) in props.tabs" :key="index" :id="`panel-${index}`" role="tabpanel"
    :aria-labelledby="`tab-${index}`" class="container-tabpanel">
    {{ panel.content }}
  </div>
  </div>
</template>


<script setup>
import { ref, watch } from 'vue'
const tabRefs = ref([])
const activeTab = ref(0)

watch(activeTab, (newValue) => {
  tabRefs.value[newValue].focus()
})
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

<style scoped>

h1{
  margin-bottom: 1.5rem;
}
.tab-container{
  max-width: 50%;
  margin: 0;
  max-height: 80%;
}
/* .container-tabpanel{
background-color: var(--switch-active);
color: var(--action-primary)
} */

.main-tablist{
  display: flex;
  gap: 0.2rem;
}
.button-tab {
  margin-bottom: 1.5rem;
  border-bottom: 3px solid transparent;
}
.button-tab[aria-selected="true"] {
  background-color: var(--border-main);
  color: var(--switch-active);
  border-bottom: 3px solid var(--action-primary);
}
</style>