<template>
  <div>
    <div v-show="tab === 1">
      <!-- 基础设置 -->
      <basic-settings :activeElement="activeElement"/>

      <hr>
      <div class="panel-row" flex>
        <div class="panel-label">文本内容</div>
        <div>
          <input
            v-model="activeElement.text"
            type="text">
        </div>
      </div>
      <div class="panel-row" flex>
        <div class="panel-label">字体</div>
        <div class="panel-value">
          <select v-model="activeElement.fontFamily">
            <option value="Arial">Arial</option>
            <option value="sans-serif">sans-serif</option>
            <option value="Microsoft YaHei">微软雅黑</option>
            <option value="Microsoft JhengHei">微软正黑体</option>
            <option value="SimHei">黑体</option>
            <option value="Hiragino Sans GB">Hiragino Sans GB</option>
            <option value="SimSun">宋体</option>
            <option value="FangSong">仿宋</option>
            <option value="PMingLiU">新细明体</option>
            <option value="KaiTi">楷体</option>
            <option value="DFKai-SB">标楷体</option>
          </select>
        </div>
      </div>
      <div class="panel-row" flex>
        <div class="panel-label">行高</div>
        <div>
          <input
            v-model="activeElement.height"
            type="number">
        </div>
        <!--<div class="panel-value">{{ activeElement.lineHeight }}</div>-->
        <!--<div class="panel-slider-wrap">-->
        <!--<vpd-slider :max="5" :min="1" v-model="activeElement.lineHeight" />-->
        <!--</div>-->
      </div>
      <div class="panel-row" flex>
        <div class="panel-label">字号</div>
        <div>
          <input
            v-model="activeElement.fontSize"
            type="number">
        </div>
        <!--<div class="panel-value">{{ activeElement.fontSize }}px</div>-->
        <!--<div class="panel-slider-wrap">-->
        <!--<vpd-slider :step="1" :max="200" :min=".85" v-model="activeElement.fontSize" />-->
        <!--</div>-->
      </div>
      <div class="panel-row" flex>
        <div class="panel-label">颜色</div>
        <div class="panel-value">{{ activeElement.color }}</div>
        <div>
          <input type="color" v-model="activeElement.color">
        </div>
      </div>
      <div class="panel-row" flex>
        <div class="panel-label">加粗</div>
        <div class="panel-value">
          <label class="form-switch">
            <input type="checkbox" v-model="activeElement.fontWeight">
            <i class="form-icon"></i>
          </label>
        </div>
      </div>
      <div class="panel-row" flex>
        <div class="panel-label">对齐</div>
        <div class="panel-value">
          <select v-model="activeElement.textAlign">
            <option value="left">左对齐</option>
            <option value="center">居中</option>
            <option value="right">右对齐</option>
          </select>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import BasicSettings from '../../CommonModule/BasicSettings'

export default {
  name: 'BasicTxtBoxStyle',
  components: {
    BasicSettings
  },
  props: ['activeElement', 'tab']
}
</script>
