<template>
  <div class="container">
    <swiper
        :slidesPerView="1"
        :spaceBetween="30"
        :breakpoints="swiperBreakPoints"
        :pagination="{
      clickable: true,
    }"
        :navigation="true"
        :modules="modules"
        class="mySwiper"
    >
      <swiper-slide v-for="(slide, index) in slides">
        <img :src="slide.url" alt="">
      </swiper-slide>
    </swiper>

  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import { Swiper, SwiperSlide } from "swiper/vue/swiper-vue";

// Import Swiper styles
import "swiper/swiper-bundle.css";

import {Pagination} from "swiper";
import {Navigation} from 'swiper'
export default {
  name: 'Home',
  components: {
    HelloWorld,
    Swiper,
    SwiperSlide,
  },
  setup() {
    return {
      modules: [Pagination,Navigation],
    };
  },
  data(){
    return {
      slides: [],
      swiperBreakPoints: {
        '640': {
          slidesPerView: 2,
          spaceBetween: 20,
        },
        '768': {
          slidesPerView: 4,
          spaceBetween: 40,
        },
        '1024': {
          slidesPerView: 5,
          spaceBetween: 50,
        },
      }
    }
  },
  async created(){
    this.slides = await (await this.axios.get('https://jsonplaceholder.typicode.com/photos?_limit=20')).data
  }
}
</script>
<style lang="scss">
.container{
  max-width: 1200px;
  margin: 0 auto;
}
.swiper-slide{
  width: 300px;
  img{
    width: 100%;
  }
}
.custom-buttons{
  display: flex;
  column-gap: 15px;
  margin-top: 30px;
}
.btn{
  background-color: #42b983;
  color: #fff;
  font-size: 18px;
  font-family: Arial,serif;
  font-weight: 500;
  border: none;
  padding: 10px 30px;
  border-radius: 10px;
}
</style>
