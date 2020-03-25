<template>
  <div class="goods">
    <good-list-item  v-for="item in goodList"  :good-item="item"/>
  </div>
</template>

<script>
import GoodListItem from './GoodListItem'
export default {
  props: {
    goodList: {
      type: Array,
      default () {
        return []
      }
    }
  },
  components: {
    GoodListItem
  }
}
</script>

<style>
  .goods {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    padding: 2px;
  }
</style>