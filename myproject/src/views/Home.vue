<template>
  <div class="home">
    <img alt="Vue logo" src="@/assets/tooth.png">
    <HelloWorld/>
    <br>
    <br>
    <bookbtn/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import bookbtn from '@/views/bookbtn'
export default {
  name: 'home',
  components: {
    HelloWorld,
    bookbtn
  }
}
</script>

<style>
img {
  height: 500px;
  width: 500px;
}
</style>