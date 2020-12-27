---
title: "Nuxtにマークダウンエディタを埋め込む"
emoji: "🌊"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["nuxt.js","Markdouwn"]
published: true
---

[vue-simplemde](https://github.com/F-loat/vue-simplemde) 
というものをありがたく使わせていただき、マークダウンエディタを埋め込んでみる。

## インストール

```
npm install vue-simplemde --save
```

## plugins配下にnuxt-simplemde-plugin.js作成

```nuxt-simplemde-plugin.js
import Vue from 'vue'
import VueSimplemde from 'vue-simplemde'
import 'simplemde/dist/simplemde.min.css'

Vue.component('vue-simplemde', VueSimplemde)
```

## nuxt.config.jsに追加

```nuxt.config.js
module.exports = {
   // some nuxt config...
   plugins: [
     { src: '~plugins/nuxt-simplemde-plugin.js', mode: 'client' },
   ],
   css: [
     'simplemde/dist/simplemde.min.css',
   ],
};
```

## コンポーネントで使用する

```main.vue
<template>
   <div class="wrap">
     <client-only>
       <vue-simplemde v-model="content" />
     </client-only>
   </div>
</template>

<script>
export default {
   data() {
     return {
       content: ''
     }
   }
}
</script>
```

## マークダウンエディタのカスタマイズ

マークダウンエディタのカスタマイズなどはconfigで設定できる。
設定項目の詳細については[こちら](https://f-loat.github.io/vue-simplemde/doc/configuration_en.html)

```main.vue
<template>
   <div class="wrap">
     <client-only>
       <vue-simplemde v-model="content" :configs="configs" />
     </client-only>
   </div>
</template>

<script>
export default {
   data:() =>( {
       content: '',
       configs: {
         autosave: {
           enabled: false
         },
         initialValue: '',
         toolbar: [
           'preview',
           '|',
           'bold',
           'italic',
           'heading',
           'heading-smaller',
           'heading-bigger',
           '|',
           'code',
           'quote',
           'link',
           '|',
           'unordered-list',
           'ordered-list',
           'table',
           'horizontal-rule',
           '|',
           'guide'
         ]
       }
   })
}
</script>
```
