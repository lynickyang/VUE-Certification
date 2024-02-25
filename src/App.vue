<script setup>
import { items } from "./movies.json";
import {ref} from "vue";
import "bootstrap-icons/font/bootstrap-icons.scss";
import CardComponent from "./compoment/Card.vue";
import ModalForm from "./compoment/Modalcompoment.vue";


const moviesJson = ref(items);


function getStartNumber(index,i) {
  console.log("觸發getStartNumber")
  console.log("index:",index)
  console.log("i:",i)
  moviesJson.value[index].rating = i;
}


</script>

<template>

  <div class="container">
    <CardComponent :movies="moviesJson" :num="5"
    @up-data="getStartNumber"
    />
    <ModalForm />
  </div>
</template>
