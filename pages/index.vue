<template>
  <div class="container">
    <div class="full-width">
      <logo />
      <h1 class="title">nuxt-test-pro</h1>
      <div class="row center">
        <h4>Please insert column count:</h4>
        <input type="text" class="col_count" v-model="colCount" />
      </div>
      <div class="row center" id="container">
        <div
          class="resize-style"
          v-for="col in getColList()"
          :key="col"
          :style="'width: '+90/colCount+'%'"
          draggable="true"
          v-on:dragstart="dragstart(col, $event)"
          v-on:dragend="dragend($event)"
          v-on:dragenter="dragenter(col, $event)"
          :id="'col_'+col"
        ></div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import Logo from "~/components/Logo.vue";

export default Vue.extend({
  components: {
    Logo
  },
  data() {
    return {
      colCount: 0,
      startX: 0,
      enterX: 0,
      dragStartId: 0,
      dragEnterId: 0
    };
  },
  methods: {
    getColList() {
      var colList = [];

      for (let index = 0; index < this.colCount; index++) {
        colList.push(index);
      }
      return colList;
    },
    dragstart(item:any, e:any) {
      this.startX = e.screenX;
      this.dragStartId = item;
    },
    dragend(e:any) {
      var startObj = document.getElementById("col_"+this.dragStartId);
      var enterObj = document.getElementById("col_"+this.dragEnterId);
      if(this.enterX < this.startX)
        startObj.parentNode.insertBefore(startObj, enterObj);
      else if(this.enterX > this.startX)
        enterObj.parentNode.insertBefore(enterObj, startObj);
    },
    dragenter(item:any, e:any) {
      this.enterX = e.screenX;
      this.dragEnterId = item;
    }
  }
});
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

.col_count {
  margin-left: 10px;
}

.full-width {
  width: 100%;
}

.center {
  justify-content: center;
}

.resize-style {
  margin: 3px;
  background-color: chocolate;
  width: 100%;
  height: 100px;
  border: 3px dotted orange;
  resize: both;
  overflow: auto;
}

[draggable] {
  -moz-user-select: none;
  -khtml-user-select: none;
  -webkit-user-select: none;
  user-select: none;
  -khtml-user-drag: element;
  -webkit-user-drag: element;
}
</style>
