<template>
  <div class="animated fadeIn">
    認証成功ページ
  </div>
</template>

<script>
export default {
  data() {
    return {
      header: {
        title: 'トップページ',
      },
    }
  },

  mounted() {
    this.setHeader();
  },

  methods: {
    setHeader() {
      this.$nuxt.$emit('setHeader', this.header);
    },
  }
}
</script>
