<script setup>
import { items } from "./movies.json";
import {ref} from "vue";
import "bootstrap-icons/font/bootstrap-icons.scss";
import CardComponent from "./compoment/Card.vue";
import ModalForm from "./compoment/Modalcompoment.vue";

const moviesJson = ref(items);//傳入card元件
const getStartNumber=(index,i)=>{//更新星星數
  moviesJson.value[index].rating = i;
}
const pushMovieJosn = (pushData)=>{//觸發pushDATA
  moviesJson.value.push(pushData);
}
const removeData = (index)=>{
  console.log("index:",index)
  moviesJson.value.splice(index,1);
  // moviesJson.value=moviesJson.value.filter((item)=>{
  //   return item !== moviesJson.value[index];
  // });
}

</script>

<template>
<!-- 監聽up-data，有收到訊息觸發後面Function -->
  <div class="container">
    <CardComponent :movies="moviesJson" @up-data="getStartNumber" @remove-data="removeData"/>
    <ModalForm @push-data="pushMovieJosn"/>
  </div>
</template>
