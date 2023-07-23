<script setup>
  import {ref, reactive, onMounted, onUnmounted} from 'vue'

  const activeIndex = ref(0)

  const carouselItems = [
    {
      image: 'https://images.pexels.com/photos/17565230/pexels-photo-17565230/free-photo-of-horse-in-meadow.jpeg?auto=compress&cs=tinysrgb&w=600',
      title: 'First Slide Title',
      caption: 'Free Rein Equine Rescue has many options and openings for Volunteers! Reach out today and start furthering our Mission of Saving Horses, Saving History!'
    },
    {
      image: 'https://images.pexels.com/photos/17565231/pexels-photo-17565231/free-photo-of-horse-in-wind.jpeg?auto=compress&cs=tinysrgb&w=600',
      title: 'Second Slide Title',
      caption: 'For questions related to your financial donations simply click here. For help in making a financial donation to Free Rein Equine Rescue Inc,'
    },
    {
      image: 'https://images.pexels.com/photos/17580594/pexels-photo-17580594/free-photo-of-black-horse-standing-against-rock-formation.jpeg?auto=compress&cs=tinysrgb&w=600',
      title: 'Third Slide Title',
      caption: 'Bring the family; plan a class outing; or simply drop by and say hi! Fill out the Contact Us on any page and let us know some dates and we will set it up for you!'
    },
    {
      image: 'https://images.pexels.com/photos/17105807/pexels-photo-17105807/free-photo-of-close-up-of-horse-head.jpeg?auto=compress&cs=tinysrgb&w=600',
      title: 'Fourth Slide Title',
      caption: 'Volunteers are the life blood of the Rescue! Please use the Contact Form on any page and indicate you are interested in volunteering!'
    }
  ]

  const imageFilter = '-webkit-filter: grayscale(100%);filter: grayscale(100%);'

  const incrementActiveIndex = () =>{
    if(activeIndex.value == carouselItems.length -1){
      activeIndex.value = 0
    }
    else{
      activeIndex.value++
    }
  }

  let timerId = null;

  const startSlideShow = function(){
    timerId = setInterval(incrementActiveIndex, 3000)
  }

  const stopSlideShow = function(){
    clearInterval(timerId)
  }

  onMounted(() => {
    startSlideShow()
  })

  onUnmounted(() =>{
    stopSlideShow()
  })
</script>

<template>
  <h4>Image Carousel by Vue JS</h4>
  <div @mouseover="stopSlideShow" @mouseleave="startSlideShow" id="carouselExampleCaptions" class="carousel">
    <div class="carousel-inner">
      <div class="carousel-item active">
        <img height="500" :src="carouselItems[activeIndex].image" class="d-block w-100 img img-responsive" alt="...">
        <div class="carousel-caption d-none d-md-block">
          <h5>{{ carouselItems[activeIndex].title }}</h5>
          <p>{{ carouselItems[activeIndex].caption }}</p>
        </div>
      </div>
    </div>
    <ul class="carousel-thumnails p-2 m-0">
      <img @click="activeIndex = index" width="50" height="50" :style="activeIndex != index?imageFilter:''" style="cursor: pointer;" class="mx-1 rounded-circle" v-for="(thumnail, index) in carouselItems" :key="index" :src="thumnail.image" alt="">
    </ul>
    <a @click.prevent="0 == activeIndex ? activeIndex = (carouselItems.length) - 1 : activeIndex--" class="carousel-control-prev" href="#" role="button">
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="sr-only">Previous</span>
    </a>
    <a @click.prevent="(carouselItems.length) - 1 == activeIndex ? activeIndex = 0 : activeIndex++" class="carousel-control-next" href="#" role="button">
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="sr-only">Next</span>
    </a>
  </div>
</template>

<style>
</style>
