<template>
  <div class="app">
    <Header />
    <div class="app-body">
      <main class="main">
        <div class="container-fluid">
          <h1 class="h4 pb-2 my-3 border-bottom border-secondary">{{ title }}</h1>
          <nuxt />
        </div>
      </main>
    </div>
  </div>
</template>

<script>
  import Header from "../components/Layout/Header/Header"
  export default {
    components: {
      Header,
    },

    data () {
      return {
        title: '',
      }
    },

    created () {
      this.$nuxt.$on('setHeader', this.setHeader)
    },

    methods: {
      setHeader(header) {
        this.title  = header.title  || '';
      }
    }

  }
</script>
