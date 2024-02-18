<script setup>
import { items } from "./movies.json";
import "bootstrap-icons/font/bootstrap-icons.scss";
import { ref, onMounted } from "vue";
import Modal from "bootstrap/js/dist/modal";

const modal = ref(null);
const myModal = ref(null);

const movies = ref(items);

function getStartNumber(index, i) {
  movies.value[index].rating = i;
}

const hideModal = () => {
  myModal.value.hide();
};
const toggleModal = () => {
  myModal.value.show();
};

onMounted(() => {
  myModal.value = new Modal(modal.value);
});
const myModal_show = () => {
  myModal.value.show();
};

const myModal_hide = () => {
  myModal.value.hide();
};
/*
 This is an Icon that you can use to represent the stars if you like
 otherwise you could just use a simple ⭐️ emoji, or * character.
*/
// import { StarIcon } from "@heroicons/vue/24/solid";
</script>

<template>
  <!-- This is where your template goes -->
  <div class="container">

    <!-- Button trigger modal -->
    <button type="button" class="btn btn-primary"  @click="myModal_show()">
      Launch static backdrop modal
    </button>

    <!-- Modal -->
    <div class="modal fade" tabindex="-1" ref="modal">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" >新增電影</h5>
            <button  type="button" class="btn-close" aria-label="Close" @click="myModal_hide"></button>
          </div>
          <div class="modal-body">
            表單放這裡
            <form>
              <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label">Email address</label>
                <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
                <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
              </div>
              <div class="mb-3">
                <label for="exampleInputPassword1" class="form-label">Password</label>
                <input type="password" class="form-control" id="exampleInputPassword1">
              </div>
              <div class="mb-3 form-check">
                <input type="checkbox" class="form-check-input" id="exampleCheck1">
                <label class="form-check-label" for="exampleCheck1">Check me out</label>
              </div>
              <button type="submit" class="btn btn-primary">Submit</button>
            </form>

          </div>

          <div class="modal-footer">
            <button type="button"  class="btn btn-secondary" @click="myModal_hide" >
              Close
            </button>
            <button type="button" class="btn btn-primary">新增</button>
          </div>
        </div>
      </div>
    </div>
    <!-- Modal end -->

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

          <img
            :src="item.image"
            class="card-img-top img-cover"
            alt="item.name"
          />
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
              <p class="card-text d-inline">Rationg:{{ item.rating }}/5</p>
              <div class="d-inline">
                <button
                  type="button"
                  v-for="i in 5"
                  :key="{ i }"
                  class="border-0"
                >
                  <div
                    class="d-inline"
                    :class="i <= item.rating ? 'text-warning' : ''"
                    @click="getStartNumber(index, i)"
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
  </div>
</template>
