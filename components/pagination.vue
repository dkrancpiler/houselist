<template>
<div v-if="totalPages() > 0" class="pagination-wrapper">
  <span v-if="showPrevious" class="pagination-btn" v-on: click="updatePage{currentpage-1}"> < </span>
  {{currentPage +1}} of {{totalPages() }}
  <span v-if="showNext" class="pagination-btn" v-on:click="updatePage(currentPage +1)"> > </span>

</div>
</template>

<script>
export default {
  name: "pagination",
  props: ['houses', 'pagination'],
  methods: {
    updatePage(pageNumber) {
      this.$emit('page:update', pageNumber)
    },
    totalPages(){
      return pagination.lastPage
      return houses.data
    },
    showPrevious() {
      return this.pagination.page == 0? false : true
    },
    showNext() {
      return this.pagination.page == (this.totalPages() -1) ? false:true;
    }
  }
}
</script>

<style scoped>

</style>
