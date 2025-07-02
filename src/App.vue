<script setup>
import { ref, computed, watchEffect } from 'vue'
import { useSeoMeta, useHead } from '@unhead/vue'

import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'

// useHead({
//   titleTemplate: title => {
//     // 當子元件傳入 title 時，使用該 title；否則，只顯示網站名稱
//     return title ? `${title} - 我的神奇網站` : '我的神奇網站'
//   },
// })

// const ogTitle = ref('When Great Minds Don’t Think Alike')
// useSeoMeta({
//   ogUrl: 'https://pgkusn.github.io/unhead-test/',
//   ogType: 'article',
//   ogTitle,
//   ogDescription: 'How much does culture influence creative thinking?',
//   ogImage:
//     'http://static01.nyt.com/images/2015/02/19/arts/international/19iht-btnumbers19A/19iht-btnumbers19A-facebookJumbo-v2.jpg',
// })

const post = ref(null)

// 透過 setTimeout 模擬非同步取得文章資料
setTimeout(() => {
  post.value = {
    title: '模擬文章標題',
    summary: '這是一段模擬的文章摘要內容。',
    coverImage: 'https://via.placeholder.com/600x300.png?text=Cover+Image',
  }
}, 3000)

useSeoMeta({
  title: () => post.value?.title || '讀取中...',
  description: () => post.value?.summary,
  ogTitle: () => post.value?.title,
  ogDescription: () => post.value?.summary,
  ogImage: () => post.value?.coverImage,
})
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
    <!-- <input type="text" v-model="ogTitle" placeholder="Enter a title for SEO" /> -->

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
