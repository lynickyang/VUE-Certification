<script setup>
import { items } from "./movies.json";
import "bootstrap-icons/font/bootstrap-icons.scss";
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
      <div v-for="item in items" :key="item.id" class="col">
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
          <div class="card-footer border-0 bg-light">
            <div class="row d-inline">
                <p class="card-text d-inline">Rationg:{{item.rating}}/5</p>
                <div v-for="i in item.rating" :key="{i}" class="row d-inline">
                  <div class="d-inline"><i class="bi bi-star-fill text-warning "></i></div>
                </div>
              </div> 
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

