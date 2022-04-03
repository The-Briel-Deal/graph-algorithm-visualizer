<template>
  <q-page class="flex flex-center">
    <DfsAndBfs />
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'
import DfsAndBfsVue from '../components/DfsAndBfs.vue'
import DfsAndBfs from '../components/DfsAndBfs.vue'

export default defineComponent({
  name: "IndexPage",
  components: { DfsAndBfs }
})
</script>
