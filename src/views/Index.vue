<template>
  <vue-page-preview
    :page="config"
    :widgets="widget"/>
</template>

<script>
import vuePagePreview from '@/components/Preview'
import Dashboard from 'Config'

export default {
  name: 'PreviewDashboard',
  components: { vuePagePreview },
  data () {
    return {
      config: null,
      widget: []
    }
  },
  created () {
    this.$nextTick(() => {
      this.getDashboardConfig()
    })
  },

  methods: {
    getDashboardConfig () {
      this.config = Dashboard.config
      this.widget = Dashboard.widget
      document.title = this.config.title
    }
  }
}
</script>
