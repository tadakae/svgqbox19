<template>
  <div class="pagination-row">
      <button class="arrow">&lt;-</button>
      <span v-for="(item, index) in new Array(10)" :key="index">
          <button class="num_page">{{index + 1}}</button>
      </span>
      <button class="arrow">-&gt;</button>
  </div>

</template>

<script>
export default {
    name: "Pagination"
}
</script>

<style scoped>

.pagination-row {
    margin-left: 540px;
    margin-top: 45px;
    margin-bottom: 150px;
}

.arrow {
    border-radius: 6px;
}

.num_page {
    border-radius: 4px;
    margin: 3px;
}

</style>