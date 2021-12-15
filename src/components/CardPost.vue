<template>
  <div class="card" >
  <div class="card-body">
    <div class="title">
      <h5 class="card-title">{{post.title}}</h5>
      <div>{{post.id}}</div>
    </div>
    <p class="card-text">{{post.body}}</p>
  </div>
</div>
</template>

<script>
export default {
  name: 'CardPost',
  props: {
    post: {}
  }
};
</script>

<style scoped>

.title {
  display: inline-flex;
  width: 100%;
}
.title >:last-child{
 position: absolute;
 right: 12px;
}
</style>
