<template>
    <div class="container">
      <TextFieldSearch v-on:filter="setField" />
      <div class="list-post" v-for="post in filteredPost" v-bind:key="post.id">
        <CardPost v-bind:post="post" />
      </div>
      <Pagination v-bind:posts="dataPosts" v-on:modifyList="modifyList" />
    </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css';
import CardPost from './components/CardPost.vue';
import TextFieldSearch from './components/TextFieldSearch.vue';
import Pagination from './components/Pagination.vue';
import axios from 'axios/dist/axios';

export default {
  name: 'App',
  components:{
    CardPost,
    TextFieldSearch,
    Pagination,
  },
  data(){
    return {
      dataPosts: [],
      filterPost: '',
      intervalPostsOne: 0,
      intervalPostsTwo: 10,
    };
  },  
  created(){
    axios({
      url: 'https://jsonplaceholder.typicode.com/posts',
      method: 'GET',
    }).then(response  => {
      this.dataPosts = response.data;
    });
  },

  methods:{
    setField(value){
      this.filterPost = value;
    },

    modifyList(args){
      this.intervalPostsOne = args.intervalPostsOne;
      this.intervalPostsTwo = args.intervalPostsTwo;
    }
  },
  computed: {
    filteredPost(){
      let list = this.dataPosts.slice(this.intervalPostsOne, this.intervalPostsTwo);
      return  this.filterPost === '' ? list : list.filter(post => (post.title.toLowerCase().includes(this.filterPost.toLowerCase())));
    },
  },
};
</script>

<style >
.list-post > *{
  margin: 8px 0; 
}
.container{
  padding-top: 50px;
}
</style>
