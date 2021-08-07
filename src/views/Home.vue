<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <WAR msg="Welcome to Your Vue.js App" />
    <Dynamo msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import WAR from "@/components/WAR.vue";
import Dynamo from "@/components/Dynamo.vue";

export default {
  name: "Home",
  components: {
    HelloWorld,
    WAR,
    Dynamo,
  },
};
</script>
