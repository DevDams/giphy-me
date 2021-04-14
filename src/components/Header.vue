<template>
  <div class="container header">
    <div class="content">
      <h1><a href="index.html">G.Gen</a></h1>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Header'
}
</script>

<style scoped>
.container {
  background-color: #131313;
  color: #fff;
  height: 70px;
  width: 100%;
  display: flex;
  align-items: center;
}

.content {
  margin-left: 10%;
}

a {
  text-decoration: none;
  color: white;
}
</style>
