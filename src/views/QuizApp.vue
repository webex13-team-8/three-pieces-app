<template>
  <h1>Vue クイズ</h1>
  <div class="app">
    <h2>Q. {{ title }}</h2>
    <img class="quiz-image" v-bind:src="imagePath" v-bind:alt="title" />
    <div class="container">
      <button
        v-for="select in selects"
        v-bind:key="select.id"
        v-on:click="clickButton(select)"
      >
        {{ select.text }}
      </button>
    </div>
    <div>{{ feedback }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "彼は人気YouTuber「東海オンエア」のメンバーです。名前は？",
      image: "ShibayuImage.jpeg",
      selects: [
        {
          id: 0,
          text: "てつや",
          isCollect: false,
          feedback: "残念！てつやはオレンジ髪が特徴です。",
        },
        {
          id: 1,
          text: "しばゆー",
          isCollect: true,
          feedback: "正解！！！！彼はしばゆーです。",
        },
        {
          id: 2,
          text: "虫眼鏡",
          isCollect: false,
          feedback: "残念！虫眼鏡は眼鏡をかけています。",
        },
      ],
      feedback: "",
    }
  },
  methods: {
    clickButton: function (select) {
      this.feedback = select.feedback
    },
  },
  computed: {
    imagePath: function () {
      return "@/assets/" + this.image
    },
  },
}
</script>

<style>
.app {
  display: flex;
  width: 100%;
  flex-direction: column;
  align-items: center;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

.quiz-image {
  height: 300px;
  width: 300px;
  object-fit: contain;
}

.container {
  display: flex;
  height: 2em;
  width: 300px;
  padding: 1em;
  justify-content: space-around;
}
</style>
