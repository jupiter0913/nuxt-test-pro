<template>
  <div class="container">
    <div>
      <logo />
      <h1 class="title">
        nuxt-test-pro
      </h1>
      <div class="row">
        <h4>Please insert column count: </h4>
        <input type="text" id="col_count" v-model="colCount"/>
      </div>
      <div class="row">
        <div class="col-style" v-for="col in getColList()" :key="col" :style="'width: '+100/colCount+'%'">
          <div class="content-style">
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import Logo from '~/components/Logo.vue'

export default Vue.extend({
  components: {
    Logo
  },
  data() {
    return {
      colCount: 0
    }
  },
  methods:{
    getColList() {
      var colList = [];

      for (let index = 0; index < this.colCount; index++) {
        colList.push(index);        
      }
      return colList;
    }
  }
})
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
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
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

.col-style {
  padding: 5px;
}
.content-style {
  background-color: chocolate;
  width: 100%;
  height: 100px;
}
</style>
