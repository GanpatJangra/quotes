<template>
  <div>
    <section class="font-Epilogue">
      <div :class="{ hidden }" class="h-[100vh] w-full bg-gray-100 flex items-center justify-center">
        <button class="flex items-center text-xl font-semibold">
          <span>loading</span>
          <svg class="ml-4 text-indigo-500 animate-spin h-7 w-7" width="24" height="24" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round" stroke-linejoin="round">
            <path stroke="none" d="M0 0h24v24H0z" />
            <path d="M9 4.55a8 8 0 0 1 6 14.9m0 -4.45v5h5" />
            <path d="M11 19.95a8 8 0 0 1 -5.3 -12.8" stroke-dasharray=".001 4.13" />
          </svg>
        </button>
      </div>
      <div class="container px-4 mx-auto">
        <div class="mb-16 h-96">
          <img class="object-cover w-full h-full rounded-lg mt-10" :src="randomimg" alt="" />
        </div>
        <div class="max-w-2xl mx-auto text-center">
          <h2 class="mb-6 text-4xl font-bold lg:text-5xl font-heading">
            {{ quotes.content }}
          </h2>
          <div class="flex items-center justify-center">
            <div>
              <h3 class="text-2xl font-bold">{{ quotes.author }}</h3>
              <p class="my-5 text-lg text-gray-500">{{ quotes.dateAdded }}</p>
              <button class="p-5 font-semibold text-white bg-blue-500 rounded-xl" @click="dataapi()">Get Quotes</button>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "index",
  data() {
    return {
      hidden: true,
      quotes: [],
      randomimg: "https://picsum.photos/800",
    };
  },
  methods: {
    async dataapi() {
      this.hidden = false;
      let min = 800;
      let max = 1200;
      let difference = max - min;
      let rand = Math.random();
      rand = Math.floor(rand * difference);
      rand = rand + min;
      this.randomimg = `https://picsum.photos/${await rand}`;
      const quotes = await this.$axios.get("https://api.quotable.io/random");
      this.quotes = quotes.data;
      this.hidden = true;
    },
  },
};
</script>
