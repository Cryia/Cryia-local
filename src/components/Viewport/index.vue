<template>
  <div
    id="viewport"
    class="holder"
    :style="preview ? screenSize : {}">
    <div
      :style="{
        backgroundColor: backgroundColor,
        backgroundImage: backPic,
        backgroundRepeat: 'no-repeat',
        width: width + 'px',
        height: height + 'px',
        position: 'relative',
        transform: 'scale(' + zoom / 100 + ')'
      }"
      class="screen"
      id="viewport-screen">

      <!-- 组件 -->
      <component
        v-for="val in widgetStore"
        :is="val.type"
        :data-title="val.name"
        :key="val.uuid"
        :val="val"
        :h="height"
        :w="width"
        :data-type="val.type"
        :data-uuid="val.uuid"
        class="layer">
        <component
          v-for="child in getChilds(val.name)"
          :is="child.type"
          :data-title="child.name"
          :key="child.uuid"
          :val="child"
          :h="height"
          :w="width"
          :data-type="child.type"
          :data-uuid="child.uuid"
          class="layer layer-child" />
      </component>
    </div>
  </div>
</template>

<script>
import vpd from '../../mixins/vpd'

export default {
  name: 'Viewport',

  mixins: [vpd],

  props: {
    'zoom': Number,
    'preview': Boolean
  },
  computed: {
    screenSize () {
      return {
        width: window.screen.width + 'px',
        height: window.screen.height + 'px',
        overflowX: this.width === window.screen.width ? 'hidden' : 'auto',
        overflowY: this.height === window.screen.height ? 'hidden' : 'auto'
      }
    },

    // 已添加的组件
    widgetStore () {
      return this.$vpd.state.widgets.filter(item => item.belong === 'page')
    },

    // 画布高度
    height () {
      return Number(this.$vpd.state.page.height)
    },

    // 页面宽度
    width () {
      return Number(this.$vpd.state.page.width)
    },

    // 页面背景色
    backgroundColor () {
      return this.$vpd.state.page.backgroundColor
    },

    // 页面背景图片
    backPic () {
      return this.$vpd.state.page.backPic
    },

    // 选中项id
    id () {
      return this.$vpd.state.uuid
    }
  },

  methods: {
    // 获取子组件
    getChilds (name) {
      return this.$vpd.state.widgets.filter(
        item => item.belong === name
      )
    }
  }
}
</script>

<style scoped>
.holder {
  width: 100%;
  height: 100%;
  overflow: auto;
  justify-content: center;
  font-size: 0;
  background-image: linear-gradient(
      45deg,
      #f5f5f5 25%,
      transparent 0,
      transparent 75%,
      #f5f5f5 0
    ),
    linear-gradient(
      45deg,
      #f5f5f5 25%,
      transparent 0,
      transparent 75%,
      #f5f5f5 0
    );
  background-position: 0 0, 13px 13px;
  background-size: 26px 26px;
  background-color: #f0f3f4;
}
.screen {
  /*margin: 25px auto;*/
  transform-origin: left top;
}
</style>
