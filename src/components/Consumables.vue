<template>
  <div class="consumables">
    <div class="consumables__bar">
      <div class="consumables__item" v-for="(x, i) in 5" :key="i">
        <!-- <vue-select 
          :options="consumables"
          label="imagePath"
        >
        </vue-select> -->
      </div>
    </div>
  </div>
</template>

<script>

import { consumablesList } from '../items/consumables'
// import vueSelect from 'vue-select'

export default {
  name: 'consumables',
  // components: { vueSelect },
  data: () => ({
    consumables: null
  }),
  mounted() {
    this.consumables = {...consumablesList}
  }
}

</script>