<template>
  <div class="fixed inset-0 z-50">
    <div class="modal-window">
      <div class="modal-content bg-info-pets">
        <div class="content_wrapper mx-auto text-center">
          <div
            class="close-btn w-12 h-12 float-right cursor-pointer p-4"
            @click="handleClose"
          ></div>
          <div class="summary-wrap">
            <div class="text-6xl text-yellow-700 font-bold my-4">
              {{ listPets[currentPet].title }}
            </div>
            <div class="text-3xl text-yellow-600">
              {{ listPets[currentPet].desc }}
            </div>
            <slider-pets :data-slider="listPets" :current-pet="currentPet" @change-slide="changeSlide" />
          </div>
          <div class="skill-wrap relative">
            <div class="font-bold text-3xl" style="color: #f3edcd;">Try Skill</div>
            <div class="text-center font-bold text-3xl my-10" style="color: #5c362c">
              {{listPets[currentPet].skill}}
            </div>
            <iframe
              width="720"
              class="aspect-video mx-auto"
              :src="listPets[currentPet].urlEmbed"
              frameborder="0"
              allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
              allowfullscreen
            ></iframe>
            <div class="text-center font-bold text-3xl mt-8 py-10" style="color: #5c362c;">
              {{listPets[currentPet].desKill}}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.bg-info-pets {
  background-image: url("../../../assets/images/pets/bg-info.jpg");
  background-repeat: no-repeat;
  background-position: 50% 0;
}
.content_wrapper {
  width: 800px;
  margin: 0 auto;
  padding-top: 100px;
}
.close-btn {
  background-image: url("../../../assets/images/close.png");
  background-repeat: no-repeat;
}
.summary-wrap {
  position: relative;
  padding: 0 30px;
  height: 886px;
}
.modal-window {
  overflow: auto;
  width: 100vw;
  height: 100vh;
  vertical-align: middle;
}
.modal-content {
  min-height: 100vh;
}
</style>
<script>
import SliderPets from "./Slider.vue";
export default {
  components: {
    SliderPets,
  },
  emits: ["handleClose"],
  props: {
    currentPet: {
      type: Number,
      default() {
        return 0;
      },
    },
    listPets: {
      type: Array,
      required: true,
    },
  },
  mounted() {
    document.querySelector("body").classList.add("overflow-hidden");
  },
  beforeDestroy() {
      document.querySelector("body").classList.remove("overflow-hidden");
  },
  emits: ['changeSlide'],
  methods: {
    handleClose() {
      this.$emit("handleClose");
    },
    changeSlide(changeCurrentPet){
        this.$emit('changeSlide',changeCurrentPet)
    }
  },
};
</script>
