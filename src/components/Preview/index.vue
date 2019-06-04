<template>
  <div class="columns col-gapless">
    <div class="viewport">
      <viewport
      preview/>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import WidgetLibrary from '@/plugins/widget'
import Viewport from '@/components/Viewport'
import vpd from '@/mixins/vpd'

export default {
  name: 'PreviewDesign',
  components: {
    Viewport
  },
  mixins: [vpd],
  props: {
    page: Object,
    widgets: Array
  },
  created () {
    Vue.use(WidgetLibrary)
  },
  watch: {
    page: {
      handler (newValue, oldValue) {
        this.$vpd.replacePage(newValue)
        this.$vpd.commit('INIT_ACTIVE')
      },
      deep: true
    },
    widgets: {
      handler (newValue, oldValue) {
        this.$vpd.replaceWidgets(newValue)
      },
      deep: true
    }
  }
}
</script>

<style lang="scss">
body {
  margin: 0;
}
.columns {
  height: 100%;
}

.viewport {
  position: relative;
  overflow: hidden;
}

.echarts {
  width: 100%;
  height:100%;
}

.layer {
  /deep/ &:hover {
    outline: 0px solid #2196f385 !important;
  }
}
</style>
