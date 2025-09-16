<template>
  <div class="q-pa-md">
    <!-- Header -->
    <q-card flat bordered class="q-mb-md">
      <div class="row items-center justify-between q-pa-sm">
        <div class="row items-center">
          <q-img src="/images/logo.png" style="width:60px; height:60px" />
          <div class="q-ml-sm text-bold text-h6">EMRAN HASMI</div>
        </div>

        <q-input
          v-model="searchText"
          placeholder="সার্চ করুন..."
          outlined
          dense
          rounded
          class="q-mx-md"
          style="width: 250px"
        />

        <div class="row items-center q-gutter-sm">
          <q-btn flat round icon="notifications" />
          <q-btn flat round icon="menu" />
        </div>
      </div>
    </q-card>

    <!-- Carousel -->
    <q-carousel
      v-model="currentSlide"
      arrows
      swipeable
      animated
      infinite
      height="220px"
      class="q-mb-lg"
    >
      <q-carousel-slide
        v-for="offer in offers"
        :key="offer.id"
        :name="offer.id"
        class="flex items-center justify-between q-pa-md bg-primary text-white"
      >
        <div>
          <h3 class="text-h6">{{ offer.title }}</h3>
          <p class="text-subtitle2">
            up to <span class="text-yellow text-bold">{{ offer.discount }}</span>%
          </p>
          <q-btn color="yellow" text-color="black" label="Buy Now" @click="buyNow(offer)" />
        </div>
        <q-img :src="offer.image" style="width:140px; height:140px; border-radius:8px" />
      </q-carousel-slide>
    </q-carousel>

    <!-- Categories -->
    <div class="row no-wrap q-mb-md q-gutter-sm scroll-x">
      <q-card
        v-for="category in categories"
        :key="category.name"
        class="q-pa-sm text-center"
        style="min-width:100px"
      >
        <q-img :src="category.image" style="width:60px; height:60px" />
        <div class="text-subtitle2 q-mt-xs">{{ category.name }}</div>
      </q-card>
    </div>

    <!-- Food Items -->
    <div>
      <h3 class="q-mb-md"> খাবার আইটেম</h3>
      <div class="row q-col-gutter-md">
        <div v-for="food in foodItems" :key="food.name" class="col-12 col-sm-6 col-md-3">
          <q-card bordered>
            <q-img :src="food.image" style="height:150px" />
            <q-card-section>
              <div class="text-h6">{{ food.name }}</div>
              <div class="text-subtitle2 text-primary">৳{{ food.price }}</div>
            </q-card-section>
            <q-card-actions align="right">
              <q-btn flat round icon="add" @click="addToCart(food)" />
            </q-card-actions>
          </q-card>
        </div>
      </div>
    </div>

    <!-- Packages as Food Items -->
    <div class="q-mt-lg">
      <h3 class="q-mb-md"> থাকা ও খাওয়ার প্যাকেজ</h3>
      <div class="row q-col-gutter-md">
        <div v-for="pkg in packages" :key="pkg.title" class="col-12 col-sm-6 col-md-3">
          <q-card bordered>
            <q-img :src="pkg.image" style="height:150px" />
            <q-card-section>
              <div class="text-h6">{{ pkg.title }}</div>
              <div class="text-subtitle2 text-primary">৳{{ pkg.price }}</div>
              <div class="text-subtitle2 q-mt-xs"><i class="fas fa-map-marker-alt"></i> {{ pkg.location }}</div>
            </q-card-section>
            <q-card-actions align="right">
              <q-btn flat round icon="add" @click="addToCart(pkg)" />
            </q-card-actions>
          </q-card>
        </div>
      </div>
    </div>

    <!-- Bottom Nav -->
    <div class="row justify-around items-center q-mt-lg bg-grey-2 q-pa-sm">
      <div v-for="nav in bottomNav" :key="nav.label" class="col text-center">
        <q-btn flat round :icon="nav.icon" />
        <div class="text-caption">{{ nav.label }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const searchText = ref("");
    const currentSlide = ref(1);

    const offers = [
      { id:1, title:"Special Pizza Offer", discount:15, image:"/images/food1.png" },
      { id:2, title:"Burger Combo Deal", discount:20, image:"/images/food2.png" },
      { id:3, title:"Weekend Hotel Stay", discount:10, image:"/images/food3.png" },
    ];

    const categories = [
      { name:"ফুড", image:"/images/food1.png" },
      { name:"থাকা ও খাওয়া", image:"/images/food2.png" },
      { name:"থাকা", image:"/images/food3.png" },
      { name:"শুধু খাওয়া", image:"/images/food4.png" },
      { name:"সেট মেনু", image:"/images/food5.png" },
    ];

    const foodItems = [
      { name:"চিকেন বিরিয়ানি", price:180, image:"/images/food1.png" },
      { name:"বিফ বার্গার", price:120, image:"/images/food2.png" },
      { name:"পিজ্জা", price:250, image:"/images/food3.png" },
      { name:"স্যান্ডউইচ", price:90, image:"/images/food4.png" },
    ];

    const packages = [
      { title: 'থাকা খাওয়া - ৩ বেলা', price: '5500/30 Days', image: '/images/package1.png', location:'বাসাবো প্যাকেট (ফ্রি লাউব্রাক)' },
      { title: 'থাকা খাওয়া - ৩ বেলা', price: '5500/30 Days', image: '/images/package2.png', location:'বাসাবো প্যাকেট (ফ্রি লাউব্রাক)' },
      { title: 'থাকা খাওয়া - ৩ বেলা', price: '5500/30 Days', image: '/images/package3.png', location:'বাসাবো প্যাকেট (ফ্রি লাউব্রাক)' },
    ];

    const bottomNav = [
      { label:"হোম", icon:"home" },
      { label:"ফুড", icon:"fastfood" },
      { label:"থাকা", icon:"hotel" },
      { label:"সেট মেনু", icon:"restaurant_menu" },
      { label:"অর্ডার", icon:"shopping_cart" },
    ];

    const buyNow = (offer)=> alert(`You selected: ${offer.title}`);
    const addToCart = (item)=> alert(`Added ${item.title || item.name} to cart!`);

    return { searchText, currentSlide, offers, categories, foodItems, packages, bottomNav, buyNow, addToCart };
  }
};
</script>

<style>
.scroll-x { overflow-x:auto; }
</style>
