<script setup>
import { items } from "./movies.json";
import "bootstrap-icons/font/bootstrap-icons.scss";
import {ref} from 'vue';

const movies = ref(items);

function getStartNumber(index,i){
  console.log("item:",index)
  console.log("i:",i)
  movies.value[index].rating=i;

}
/*
 This is an Icon that you can use to represent the stars if you like
 otherwise you could just use a simple ⭐️ emoji, or * character.
*/
// import { StarIcon } from "@heroicons/vue/24/solid";
</script>

<template>
  <!-- This is where your template goes -->
  <div class="container">
    <div class="row row-cols-3 my-4">
      <div v-for="( item,index ) in movies" :key="item.id" class="col">
        <div class="card">
          <img
            :src="item.image"
            class="card-img-top img-cover"
            alt="item.name"
          />
          <div class="card-title mb-0">
            <p class="fs-3 fw-bold m-3 mb-0 ">
              {{ item.name }}
            </p>
          </div>
          <div class="card-body word-height pt-0">
            <div v-for="genres in item.genres" :key="index" class="card-text d-inline ">
              <span class="badge rounded-pill text-bg-primary mx-1">{{ genres }}</span>
            </div>
            <p class="card-text mt-3">
              {{ item.description }}
            </p>
          </div>
          <div class="card-footer border-0 ">
            <div class="row d-inline">
                <p class="card-text d-inline">Rationg:{{item.rating}}/5</p>
                <div class="d-inline">
                  <button v-for="i in 5" :key="{i}" >
                    <div class="d-inline" 
                    :class="i<= item.rating? 'text-warning': ''"
                    @click="getStartNumber(index,i)"
                    >
                    <i class="bi bi-star-fill "></i>
                    </div>
                  </button>
                </div>
              </div> 
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

