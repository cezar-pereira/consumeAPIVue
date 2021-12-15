<template>

<div>
  <nav aria-label="...">
      <ul class="pagination justify-content-center " >
        <li class="page-item" v-bind:class="{disabled:currentPage === 1}" v-on:click="previusPage"><span class="page-link">Anterior</span></li>
        <div v-for="page in numberOfPages" v-bind:key="page">
          <li class="page-item" v-bind:class="{active: (page === currentPage)}" v-on:click="changePage(page)"><span class="page-link">{{page}}</span></li>
        </div>
        <li class="page-item" v-bind:class="{disabled: currentPage === numberOfPages}" v-on:click="nextPage"><span class="page-link">Próxima</span></li>
      </ul>
  </nav>
</div>

</template>

<script>
export default {
  props: {
    posts:[],
  },
  data(){
    return {
      itemsPerPage: 10,
      numberOfPages: 0,
      currentPage: 1
    };
  },
  watch:{
    posts:{
      deep: true,
      immediate: true,
      handler(){
        this.numberOfPages = Math.ceil((this.posts.length) / this.itemsPerPage);
      }
    },
  },
  methods:{
    changePage(page){
      this.currentPage = page;
      this.eventChangePage();
    },
    previusPage(){
      if(this.currentPage != 1)
        this.changePage(--this.currentPage);
    },
    nextPage(){
      if(this.currentPage != this.numberOfPages)
        this.changePage(++this.currentPage);
    },
    eventChangePage(){
      if(this.currentPage === 0)
        this.$emit('modifyList', {'intervalPostsOne': 0, 'intervalPostsTwo': (this.currentPage * this.itemsPerPage)});
      else
        this.$emit('modifyList', {'intervalPostsOne': ((this.currentPage-1) * this.itemsPerPage), 'intervalPostsTwo': (this.currentPage * this.itemsPerPage)});
    }
  }
};
</script>

<style>
span.page-link:hover{
  cursor: pointer;
}
</style>