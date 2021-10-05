<template>
  <div @click="fire" :class="`${filter} filter-item`" :style="{backgroundImage : `url(${url})`}">
      <slot></slot>
  </div>
</template>

<script>
export default {
    name : 'filterbox',
    methods: {
        fire() {
            this.emitter.emit('filter',this.filter);
        }
    },
    props : {
        url : String,
        filter : String,
    }


}
</script>

<style>
.filter-item {
  width: 100px;
  height: 100px;
  margin: 10px 10px 10px auto;
  padding: 8px;
  display: inline-block;
  color : white;
  background-size: cover;
  background-position : center;
}
</style>