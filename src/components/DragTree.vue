<template>
  <draggable :list="menus" :forceFallback="true" handle=".handle">
    <div v-for="(item, i) in menus" :key="i">
      <div class="menu">
        <div class="input">
          <el-button
            :icon="`el-icon-arrow-${item.expanding? 'down':'right'}`"
            size="mini"
            type="text"
            @click="item.expanding = !item.expanding;$forceUpdate()"
            v-if="item.subs && item.subs.length"
          />
          <el-input
            :disabled="!isEditing"
            v-model="item.name"
            size="mini"
            style="display: inline-block;width: 200px;"
            placeholder="请输入看板名"
          />
        </div>
        <div class="btns" v-show="isEditing">
          <el-button
            v-if="item.level < maxLevel"
            type="text"
            @click="addChild(item.subs);item.expanding = true"
            icon="el-icon-plus"
          />
          <el-button type="text" @click="del(list, i)" icon="el-icon-delete" />
          <Iconfont class="handle" name="drag-list" />
        </div>
      </div>
      <DragTree
        :list="item.subs"
        class="sub-tree"
        v-show="item.expanding"
        :expandAll="expandAll"
        :level="level+1"
        :isEditing="isEditing"
      />
    </div>
  </draggable>
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: "DragTree",
  props: {
    list: {
      type: Array,
      default: () => []
    },
    isEditing: {
      type: Boolean,
      default: false
    },
    expandAll: {
      type: Boolean,
      default: false
    },
    level: {
      type: Number,
      default: 1
    },
    maxLevel: {
      type: Number,
      default: 3
    }
  },
  computed: {
    menus() {
      this.list.forEach(item => {
        item.level = this.level;
        item.expanding = this.expandAll;
      });

      return this.list;
    }
  },
  components: {
    draggable
  },
  methods: {
    addChild(list) {
      list.push({
        name: "",
        subs: [],
        expanding: false
      });
    },
    del(list, index) {
      console.log("list", list, index);
      list.splice(index, 1);
    }
  }
};
</script>
<style scoped>
.menu {
  display: grid;
  /* grid-template-columns: repeat(12, 1fr); */
  /* grid-template-rows: repeat(2, 1fr); */
  grid-template-columns: 1fr 100px;
}

.sub-tree {
  padding-left: 25px;
}
.input,
.btns {
  height: 40px;
  line-height: 40px;
}
.handle {
  cursor: move;
  margin: 0 10px;
}

.sortable-drag {
  /* 拖拽的dom */
  /* background: red; */
}
.sortable-ghost {
  /* 在拖放位置放下的dom */
}
</style>