<template src="./StockSelector.html"></template>

<script>
import { stocksToBuy } from '../../data/data'

export default {
  data() {
    return {
      selected: [],
      options: stocksToBuy,
    }
  },
  computed: {
    showSelector() {
      return this.$store.getters.getShowTable
    }
  },
  methods: {
    resetStock() {
      console.log('resetStock')

      this.selected = []
      this.$store.dispatch('getStock', [])
    },
    stockSelected() {
      setTimeout(() => {
        let suma = 0
        this.$store.dispatch('getStock', this.selected)
        const selectedShops = this.$store.getters.getSelectedShops
        const selectedStocks = this.$store.getters.getStocksSelected

        selectedShops.forEach(shop => {
          selectedStocks.forEach(stock => (suma += shop[stock]))
          shop.total = suma
          suma = 0
        })

        this.$store.dispatch('addTotal', selectedShops)
      }, 0)
    }
  }
}
</script>

<style scoped>
div {
  color: white
}
</style>
