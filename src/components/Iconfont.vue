<template>
    <svg class="iconfont" aria-hidden="true"
        :width="width"
        :height="height"
        :style="{color}"
    >
        <use :xlink:href="iconName"></use>
    </svg>
</template>

<script>
const defaultSize = '1em'
export default {
  props: {
    width: {
      default: defaultSize
    },
    height: {
      default: defaultSize
    },
    color: {
      type: String
    },
    name: {
      type: String
    }
  },
  computed: {
    iconName () {
      return `#icon-${this.name}`
    }
  }

}
</script>
<style >
.iconfont {
    fill: currentColor;
    vertical-align: -0.15em;
}
</style>
