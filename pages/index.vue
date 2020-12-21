<template>
  <div class="animated fadeIn">
    <b-row>
      <b-col md="12">
        <b-button variant="primary" @click="displayUsers">User表示</b-button>
      </b-col>
    </b-row>
    <p class="my-3 h4 font-weight-bold text-primary">{{ count }}件</p>
    <div v-if="isLoading" class="text-center">
      <b-spinner variant="primary" label="Spinning"></b-spinner>
    </div>
    <b-row v-if="items.length !== 0">
      <b-col lg="12">
        <b-card v-for="(item, index) in items" class="mb-4">
          <div slot="header" class="font-weight-bold">
            User{{ index + 1 }}
          </div>
          <b-card-body class="py-0 px-2">
            <p class="my-3"><span class="font-weight-bold">ID: </span>{{ item.id }}</p>
            <p class="my-3"><span class="font-weight-bold">物件名: </span>{{ item.name }}</p>
          </b-card-body>
        </b-card>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      header: {
        title: 'サンプルページ',
      },
      count: 0,
      items: [],
      isLoading: false,
    }
  },

  mounted() {
    this.setHeader();
  },

  methods: {
    setHeader() {
      this.$nuxt.$emit('setHeader', this.header);
    },

    async displayUsers() {
      this.isLoading = true;

      try {
        const res = await this.$axios.get('/api/admin/users');

        this.count = res.data.length;
        this.items = res.data;

      } catch (e) {
        console.log(e);
      }
      this.isLoading = false;
    },
  }
}
</script>
