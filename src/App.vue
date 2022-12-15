<template>
  <div class="container inner">
    <form @submit.prevent>
      <Header />
      <Main />
    </form>
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import Main from "@/components/Main.vue";
export default {
  name: "App",

  components: {
    Header,
    Main,
  },
};
</script>

<style>
.container {
  width: 1200px;
  margin: 0 auto;
  padding: 20px 50px;
}
body {
  padding: 0;
  margin: 0;
  font-family: sans-serif;
  font-size: 18px;
}
.inner {
  margin-top: 50px;
  border: 2px solid rgb(212, 212, 212);
}
.input {
  font-size: 18px;
  padding: 10px 5px;
  margin-right: 10px;
}
.btn {
  position: relative;
  padding: 12px 20px;
  border: 1px solid rgb(212, 212, 212);
  cursor: pointer;
}
.btn::before {
  position: absolute;
  content: "";
  background: url("./img/btn_icon.svg") no-repeat center center;
  background-size: cover;
  padding: 13px;
  top: 9px;
  left: 5px;
}
</style>
