<template>
    <div class="input-group mb-3">
        <!-- @input="$event.target.composing = false" for realtime time search in android keybor -->
        <input type="text" class="form-control" placeholder="Pesquisa por título" aria-describedby="basic-addon1" @input="$event.target.composing = false" v-model="search">
    </div>
</template>

<script>
export default {
  name: 'TextFieldSearch',
  data(){
    return {
      search: '',
    };
  },
  watch:{
    search:{
      deep: true,
      immediate: true,
      handler(){
        this.$emit('filter', this.search);
      }
    }
  }
  
};
</script>