<template>
    <div>
      <v-btn v-on:click="refresh" >Обновить список</v-btn>
        <ul>
            <Order v-bind:sales="sales" />
        </ul>
    </div>
</template>

<script>
import Order from '@/components/Order'

export default {
  components: {Order},
  async fetch({store}) {
    if (store.getters['orders/sales'].length === 0) {
      await store.dispatch('orders/fetch')
    }
  },
  computed: {
    sales() {
        return this.$store.getters['orders/sales'];
    }
  },
  methods: {
    async refresh() {
      await this.$store.dispatch('orders/fetch')
      await this.$store.dispatch('refresh')
    }
  }
}
</script>