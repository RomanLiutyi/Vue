<template>
  <div>
    <h1 class="title">{{ title }}</h1>
  </div>
</template>
<script>
export default {
    props: { title: String },
};
</script>
<style >
.title {
  width: 100%;
  padding: 0;
  margin: 0;
  font-size: 1.8rem;
  color: #cff;
}
</style>