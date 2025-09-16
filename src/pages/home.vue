<template>
  <div class="q-pa-md">
    <!-- Header -->
    <q-card flat bordered class="q-mb-md">
      <div class="row items-center justify-between q-pa-sm">
        <!-- Logo -->
        <div class="row items-center">
          <q-img
            src="~src/assets/Screenshot from 2025-01-09 15-51-47.png"
            style="width: 60px; height: 60px"
          />
          <div class="q-ml-sm text-bold text-h6">EMRAN HASMI</div>
        </div>

        <!-- Search -->
        <q-input
          v-model="searchText"
          placeholder="সার্চ করুন..."
          outlined
          dense
          rounded
          class="q-mx-md"
          style="width: 250px"
        />

        <!-- Icons -->
        <div class="row items-center q-gutter-sm">
          <q-btn flat round icon="notifications" />
          <q-btn flat round icon="menu" />
        </div>
      </div>
    </q-card>

    <!-- Special Offers Carousel -->
    <q-carousel
      v-model="currentSlide"
      animated
      arrows
      infinite
      swipeable
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
            up to
            <span class="text-yellow text-bold">{{ offer.discount }}</span
            >%
          </p>
          <q-btn
            color="yellow"
            text-color="black"
            label="Buy Now"
            class="q-mt-sm"
            @click="buyNow(offer)"
          />
        </div>
        <q-img
          :src="offer.image"
          style="width: 140px; height: 140px; border-radius: 8px"
        />
      </q-carousel-slide>
    </q-carousel>

    <!-- Categories -->
    <div class="row no-wrap q-mb-md q-gutter-sm scroll-x">
      <q-card
        v-for="category in categories"
        :key="category.name"
        class="q-pa-sm text-center"
        style="min-width: 100px"
      >
        <q-img :src="category.image" style="width: 60px; height: 60px" />
        <div class="text-subtitle2 q-mt-xs">{{ category.name }}</div>
      </q-card>
    </div>

    <!-- Food Items -->
    <div>
      <h3 class="q-mb-md">খাবার আইটেম</h3>
      <div class="row q-col-gutter-md">
        <div
          v-for="food in foodItems"
          :key="food.name"
          class="col-12 col-sm-6 col-md-3"
        >
          <q-card bordered>
            <q-img :src="food.image" style="height: 150px" />
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
  name: "HomePage",
  setup() {
    const searchText = ref("");
    const currentSlide = ref(1);

    const offers = [
      {
        id: 1,
        title: "Special Pizza Offer",
        discount: 15,
        image: "https://via.placeholder.com/150/ff7f7f/000000",
      },
      {
        id: 2,
        title: "Burger Combo Deal",
        discount: 20,
        image: "https://via.placeholder.com/150/7fcfff/000000",
      },
      {
        id: 3,
        title: "Weekend Hotel Stay",
        discount: 10,
        image: "https://via.placeholder.com/150/7fff7f/000000",
      },
    ];

    const categories = [
      { name: "ফুড", image: "https://via.placeholder.com/60" },
      { name: "থাকা ও খাওয়া", image: "https://via.placeholder.com/60" },
      { name: "শুধু খাওয়া", image: "https://via.placeholder.com/60" },
      { name: "সেট মেনু", image: "https://via.placeholder.com/60" },
    ];

    const foodItems = [
      {
        name: "চিকেন দম বিরিয়ানি",
        price: 180,
        image: "https://via.placeholder.com/200x120",
      },
      {
        name: "চিকেন রোস্ট",
        price: 120,
        image: "https://via.placeholder.com/200x120",
      },
      {
        name: "বাসমতি কাচ্চি",
        price: 250,
        image: "https://via.placeholder.com/200x120",
      },
      {
        name: "বিফ তেহারি",
        price: 200,
        image: "https://via.placeholder.com/200x120",
      },
    ];

    const bottomNav = [
      { label: "হোম", icon: "home" },
      { label: "ফুড আইটেমস", icon: "fastfood" },
      { label: "থাকা ও খাওয়া", icon: "hotel" },
      { label: "সেট মেনু", icon: "restaurant_menu" },
      { label: "অর্ডার", icon: "shopping_cart" },
    ];

    const buyNow = (offer) => {
      alert(`You selected: ${offer.title}`);
    };

    const addToCart = (food) => {
      alert(`Added ${food.name} to cart!`);
    };

    return {
      searchText,
      currentSlide,
      offers,
      categories,
      foodItems,
      bottomNav,
      buyNow,
      addToCart,
    };
  },
};
</script>

<style>
.scroll-x {
  overflow-x: auto;
}
</style>
