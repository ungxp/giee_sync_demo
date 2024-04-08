<script setup>
const url =
  "https://fuss10.elemecdn.com/a/3f/3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg";
const srcList = [
  "https://fuss10.elemecdn.com/a/3f/3302e58f9a181d2509f3dc0fa68b0jpeg.jpeg",
  "https://fuss10.elemecdn.com/1/34/19aa98b1fcb2781c4fba33d850549jpeg.jpeg",
  "https://fuss10.elemecdn.com/0/6f/e35ff375812e6b0020b6b4e8f9583jpeg.jpeg",
  "https://fuss10.elemecdn.com/9/bb/e27858e973f5d7d3904835f46abbdjpeg.jpeg",
  "https://fuss10.elemecdn.com/d/e6/c4d93a3805b3ce3f323f7974e6f78jpeg.jpeg",
  "https://fuss10.elemecdn.com/3/28/bbf893f792f03a54408b3b7a7ebf0jpeg.jpeg",
  "https://fuss10.elemecdn.com/2/11/6535bcfb26e4c79b48ddde44f4b6fjpeg.jpeg",
];
import instance from "./service/index";
import { v4 as uuidv4 } from "uuid";
import { ref, onMounted, onUnmounted } from "vue";
const svg = ref("");
let uuid = ref("");
const getCaptcha = () => {
  instance
    .get("/api/login/getCaptcha", {
      params: {
        sid: localStorage.getItem("sid"),
      },
    })
    .then((res) => {
      console.log("res", res);
      svg.value = res.data.data;
    });
};
onMounted(() => {
  if (localStorage.getItem("sid")) {
    uuid.value = localStorage.getItem("sid");
  } else {
    uuid.value = uuidv4();
    localStorage.setItem("sid", uuid.value);
  }
});
</script>

<template>
  <div @click="getCaptcha">111</div>
  <div v-html="svg"></div>
  <el-image
    style="width: 100px; height: 100px"
    :src="url"
    :zoom-rate="1.2"
    :max-scale="7"
    :min-scale="0.2"
    :preview-src-list="srcList"
    :initial-index="4"
    fit="cover"
  />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
