<template>
  <div class="result">
    <div class="title">{{ title }}</div>
    <div class="desc">{{ description }}</div>
  </div>
</template>

<script>
export default {
  name: "AppResult",

  props: {
    results: {
      type: Array,
      required: true
    },

    totalCorrect: {
      type: Number,
      required: true
    }
  },

  computed: {
    title() {
      return this.results[this.resultIndex].title;
    },
    description() {
      return this.results[this.resultIndex].desc;
    },
    resultIndex() {
      let resIndex = 0;

      this.results.forEach((item, index) => {
        if (item.min <= this.totalCorrect && item.max >= this.totalCorrect)
          resIndex = index;
      });

      return resIndex;
    }
  }
};
</script>
