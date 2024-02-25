<script setup>

defineProps(['movies'])
defineEmits(['up-data']);
// const emit = defineEmits(['up-data']);

// const upDateStart=(index,i)=>{
//   emit('up-data',index,i );
// }

// function upDateStart(index,i){
//   console.log("觸發點及index是",index);
//   console.log("觸發點及i是",i);
//   emit('up-data',index,i );
// }
</script>

<template>
  <div class="row row-cols-3 my-4">
    <div v-for="(item, index) in movies" :key="item.id" class="col">
      <div class="card position-relative">
        <div class="position-absolute top-0 end-0 p-1 mx-2">
          <i
            class="bi bi-star-fill fs-1"
            :class="item.rating >= 1 ? 'text-warning' : ''"
          ></i>
        </div>
        <div class="z-3 position-absolute top-0 end-0 fs-5 mx-4 my-3">
          <span>{{ item.rating }}</span>
        </div>

        <img :src="item.image" class="card-img-top img-cover" alt="item.name" />
        <div class="card-title mb-0">
          <p class="fs-3 fw-bold m-3 mb-0">
            {{ item.name }}
          </p>
        </div>
        <div class="card-body word-height pt-0">
          <div
            v-for="genres in item.genres"
            :key="index"
            class="card-text d-inline"
          >
            <span class="badge rounded-pill text-bg-primary mx-1">{{
              genres
            }}</span>
          </div>
          <p class="card-text mt-3">
            {{ item.description }}
          </p>
        </div>
        <div class="card-footer border-0">
          <div class="row d-inline">
            <p class="card-text d-inline">Rating:{{ item.rating }}/5</p>
            <div class="d-inline">
              <button
                type="button"
                v-for="i in 5"
                :key="{ i }"
                class="border-0"
                @click="$emit('up-data',index,i );"
              >
                <div
                  class="d-inline"
                  :class="i <= item.rating ? 'text-warning' : ''"
                >
                  <i class="bi bi-star-fill"></i>
                </div>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
