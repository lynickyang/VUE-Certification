<script setup>
import { items } from "./movies.json";
import "bootstrap-icons/font/bootstrap-icons.scss";
import { ref, onMounted } from "vue";
import Modal from "bootstrap/js/dist/modal";

const modal = ref(null);
const myModal = ref(null);

const movies = ref(items);

const addMovie={
  id:"",
  name:"",
  description:"",
  iamge:"",
  rating:0,
  genres:[],
  inTheaters:false,
}

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
    <button type="button" class="btn btn-primary" @click="myModal_show()">
      Launch static backdrop modal
    </button>

    <!-- Modal -->
    <div class="modal fade" tabindex="-1" ref="modal">
      <div class="modal-dialog modal-lg">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">新增電影</h5>
            <button
              type="button"
              class="btn-close"
              aria-label="Close"
              @click="myModal_hide"
            ></button>
          </div>
          <div class="modal-body">
            <form class="row g-3">
              <div class="mb-3">
                <label for="name" class="form-label">電影名稱</label>
                <input  type="text" class="form-control" id="name" />

              </div>

              <div class="mb-3">
                <label for="description" class="form-label">影片描述</label>
                <textarea
                  class="form-control"
                  id="description"
                  rows="3"
                ></textarea>
              </div>

              <div class="mb-3">
                <label for="image" class="form-label">照片上傳</label>
                <input
                  type="text"
                  class="form-control"
                  id="image"
                  aria-describedby="imagehelp"
                />
                <div id="imagehelp" class="form-text">請輸入圖片的網址</div>
              </div>
              <div class="col-md-4">
                <label for="rating" class="form-label">評分（1-5）</label>
                <select id="rating" class="form-select form-select-sm" aria-label="Small select example">
                  <option selected disabled>評分</option>
                  <option value="1">1</option>
                  <option value="2">2</option>
                  <option value="3">3</option>
                  <option value="4">4</option>
                  <option value="5">5</option>
                </select>
              </div>

              <div class="col-md-4">
                <label class="form-check-label" >電影類型</label>
                <div class="form-check">
                  <input class="form-check-input" type="checkbox" value="Action" id="Action">
                  <label class="form-check-label" for="Action">Action</label>
                </div>

                <div class="form-check">
                  <input class="form-check-input" type="checkbox" value="Crime" id="Crime">
                  <label class="form-check-label" for="Crime">Crime</label>
                </div>

                <div class="form-check">
                  <input class="form-check-input" type="checkbox" value="Drama" id="Drama">
                  <label class="form-check-label" for="Drama">Drama</label>
                </div>
              </div>

              <div class="col-md-4">
                <label class="form-check-label" >院線片嗎</label>
                <div class="form-check">
                  <input class="form-check-input" type="radio" name="inTheaters" id="inTheaters">
                  <label class="form-check-label" for="inTheaters">
                    已經上映
                  </label>
                </div>
                <div class="form-check">
                  <input class="form-check-input" type="radio" name="inTheaters" id="NotinTheaters" checked>
                  <label class="form-check-label" for="NotinTheaters">
                    即將上映
                  </label>
                </div>
              </div>

              <button type="submit" class="btn btn-primary">Submit</button>
            </form>
          </div>

          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              @click="myModal_hide"
            >
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
