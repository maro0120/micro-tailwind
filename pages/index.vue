<template>
<div class="min-h-screen flex flex-col font-index">
<nav class="flex items-center justify-between flex-wrap bg-teal-500 p-6">
  <div class="flex items-center flex-shrink-0 text-white mr-6">
    <svg class="fill-current h-8 w-8 mr-2" width="54" height="54" viewBox="0 0 54 54" xmlns="http://www.w3.org/2000/svg"><path d="M13.5 22.1c1.8-7.2 6.3-10.8 13.5-10.8 10.8 0 12.15 8.1 17.55 9.45 3.6.9 6.75-.45 9.45-4.05-1.8 7.2-6.3 10.8-13.5 10.8-10.8 0-12.15-8.1-17.55-9.45-3.6-.9-6.75.45-9.45 4.05zM0 38.3c1.8-7.2 6.3-10.8 13.5-10.8 10.8 0 12.15 8.1 17.55 9.45 3.6.9 6.75-.45 9.45-4.05-1.8 7.2-6.3 10.8-13.5 10.8-10.8 0-12.15-8.1-17.55-9.45-3.6-.9-6.75.45-9.45 4.05z"/></svg>
    <span class="font-semibold text-xl tracking-tight">Tailwind CSS</span>
  </div>
  <div class="block lg:hidden">
    <button class="flex items-center px-3 py-2 border rounded text-teal-200 border-teal-400 hover:text-white hover:border-white">
      <svg class="fill-current h-3 w-3" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><title>Menu</title><path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z"/></svg>
    </button>
  </div>
  <div class="w-full block flex-grow lg:flex lg:items-center lg:w-auto">
    <div class="text-sm lg:flex-grow">
      <a href="#responsive-header" class="block mt-4 lg:inline-block lg:mt-0 text-teal-200 hover:text-white mr-4">
        Docs
      </a>
      <a href="#responsive-header" class="block mt-4 lg:inline-block lg:mt-0 text-teal-200 hover:text-white mr-4">
        Examples
      </a>
      <a href="#welcome" class="block mt-4 lg:inline-block lg:mt-0 text-teal-200 hover:text-white">
        welcome
      </a>
    </div>
  </div>
</nav>
  <div class="hero-container bg-cover bg-center" :style="{'background-image': `url(${require('@/assets/img/41447317.jpg')})`}"">
    <div>
      <Logo />
      <h1 class="title">
        micro-tailwind
      </h1>
    </div>
  </div>
  <div class="container mx-auto px-6 pt-20">
    <article class="pb-20">
      <h2 class="pb-5 lg:px-32 text-base sm:text-xl lg:text-4xl text-center text-orange-600">お知らせ</h2>
      <div v-for="content in contents" :key="content.id" class="lg:px-32 sm:text-xl xl:text-2xl">
        <nuxt-link :to="`/${content.id}`" class="flex items-center mb-4 hover:opacity-75">
          <div class="w-1/4 bg-gray-400 h-12 flex items-center"><p>{{ content.createdAt | moment }}</p></div>
          <div class="w-3/4 bg-gray-500 h-12 flex items-center">{{ content.title }}</div>
        </nuxt-link>
      </div>
    </article>
  </div>
  <div class="container mx-auto px-6">
    <article id="welcome" class="pb-20">
      <h2 class="pb-5 lg:px-32 text-base sm:text-xl lg:text-4xl text-center text-orange-600">
        ようこそ<br class="lg:hidden">おいしさいっぱいの<br>フルフルヴィレッジへ
      </h2>
      <p class="lg:px-32 pb-1 text-lg leading-4">
        フルフルが大切にしていること「安心安全」「おいしい」「楽しい」地域の心がふれあう憩いの場。家族団らんの風景を造りたい。そんな想いのVillageです。
      </p>
    </article>
  </div>
</div>
</template>

<script>
export default {}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS */
.hero-container {
  @apply min-h-screen flex justify-center items-center text-center;
}
.title {
  @apply font-index block font-light text-6xl text-blue-900 tracking-widest;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
<script>
import axios from 'axios'
import moment from 'moment';
export default {
  filters: {
        moment: function (date) {
            return moment(date).format('YYYY/MM/DD');
        }
    },
  async asyncData({ $config }) {
    const { data } = await axios.get(
      // your-service-id部分は自分のサービスidに置き換えてください
      'https://rantan.microcms.io/api/v1/blogs',
      {
        // your-api-key部分は自分のapi-keyに置き換えてください
        headers: { 'X-API-KEY':$config.apiKey }
      }
    )
    return data
  }
}
</script>
