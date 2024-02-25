
<script setup>
import { ref, onMounted } from "vue";
import * as bootstrap from 'bootstrap'
const emit = defineEmits(['push-data']);

const modal = ref(null);
const myModal = ref(null);

const myModal_show = () => {
  myModal.value.show();
};

const myModal_hide = () => {
  myModal.value.hide();
};

onMounted(() => {
  myModal.value = new bootstrap.Modal(modal.value);
});

const newData = ref({
  name:"",
  description:'',
  image:'',
  rating:0,
  genres:[],
  inTheaters:false,
}
)

const cleanForm =()=>{
  newData.value.name="",
  newData.value.description="",
  newData.value.image="",
  newData.value.rating=0,
  newData.value.genres=[],
  newData.value.inTheaters=false
}

const submitForm =()=>{
  // console.log("submit click")
  // console.log(newData.value)
  let pushData= {
    id:new Date().valueOf(),
    name:newData.value.name,
    description:newData.value.description,
    image:newData.value.image,
    rating:newData.value.rating,
    genres:newData.value.genres,
    inTheaters:newData.value.inTheaters,
  }
  // console.log(pushData)
  emit('push-data',pushData)
  //movies.value.push(pushData)
  cleanForm();
  myModal_hide();
}

</script>

<template>
  <!-- Button trigger modal -->
  <button type="button" class="btn btn-primary" @click="myModal_show()">
    新增電影資料
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
            <!-- <form @submit.prevent="submitForm" class="row g-3"></form> -->
            <div class="mb-3">
              <label for="name" class="form-label">電影名稱</label>
              <input
                v-model="newData.name"
                type="text"
                class="form-control"
                id="name"
              />
              {{ newData.name }}
            </div>

            <div class="mb-3">
              <label for="description" class="form-label">影片描述</label>
              <textarea
                v-model="newData.description"
                class="form-control"
                id="description"
                rows="3"
              ></textarea>
              {{ newData.description }}
            </div>

            <div class="mb-3">
              <label for="image" class="form-label">照片上傳</label>
              <input
                v-model="newData.image"
                type="text"
                class="form-control"
                id="image"
                aria-describedby="imagehelp"
              />
              <div id="imagehelp" class="form-text">
                請輸入圖片的網址{{ newData.image }}
              </div>
            </div>
            <div class="col-md-4">
              <label for="rating" class="form-label">評分（1-5）</label>
              <select
                v-model="newData.rating"
                id="rating"
                class="form-select form-select-sm"
                aria-label="Small select example"
              >
                <option selected disabled>評分</option>
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
                <option value="5">5</option>
              </select>
              <p>{{ newData.rating }}</p>
            </div>

            <div class="col-md-4">
              <label class="form-check-label">電影類型</label>
              <div class="form-check">
                <input
                  v-model="newData.genres"
                  class="form-check-input"
                  type="checkbox"
                  value="Action"
                  id="Action"
                />
                <label class="form-check-label" for="Action">Action</label>
              </div>

              <div class="form-check">
                <input
                  v-model="newData.genres"
                  class="form-check-input"
                  type="checkbox"
                  value="Crime"
                  id="Crime"
                />
                <label class="form-check-label" for="Crime">Crime</label>
              </div>

              <div class="form-check">
                <input
                  v-model="newData.genres"
                  class="form-check-input"
                  type="checkbox"
                  value="Drama"
                  id="Drama"
                />
                <label class="form-check-label" for="Drama">Drama</label>
              </div>
              {{ newData.genres }}
            </div>

            <div class="col-md-4">
              <div class="form-check">
                <input
                  v-model="newData.inTheaters"
                  class="form-check-input"
                  type="checkbox"
                  value="Drama"
                  id="Drama"
                />
                <label class="form-check-label" for="Drama">已上映</label>
              </div>
              {{ newData.inTheaters }}
            </div>

            <!-- <button type="submit" class="btn btn-primary">Submit</button> -->
          </form>
        </div>

        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" @click="myModal_hide">
            Close
          </button>
          <button @click="cleanForm" type="button" class="btn btn-primary">
            清除
          </button>
          <button @click="submitForm" type="submit" class="btn btn-primary">
            新增
          </button>
        </div>
      </div>
    </div>
  </div>
  <!-- Modal end -->
</template>
