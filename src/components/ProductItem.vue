<template>
  <div class="ProductItem--Inline">
    <div
      @click="goToProductDetail(product.id)"
      :class="[bgColor, txtColor]"
    >
      {{ product.name }} ({{ product.quantity }})
    </div>
    <div> 
      {{ product.price | toLocalePrice | toPrice }}
    </div>
    <button @click="addToShopCart(product.price, product.id)">
      Agregar al carrito
    </button>
  </div>
</template>

<script>
import * as Filters from '@/utils/filters';

export default {
  name: "ProductItem",
  props: {
    product: Object,
    addToShopCart: Function,
  },
  data () {
    return {
      bgColor: "ProductItem--bgColor-green",
      txtColor: "ProductItem__Text--white",
    }
  },
  methods: {
    goToProductDetail (id) {
      this.$router.push({
        name: 'productDetail',
        params: {
          id,
        }
      });
    }
  },
  filters: {
    toPrice: Filters.toPrice,
    toLocalePrice: Filters.toLocalePrice,
  }
}
</script>

<style lang="less" scoped>
@import "../stylesheet/colors.less";

.ProductItem {
  &--inline {
    display: flex;
    justify-content: space-evenly;
  }
  &__Text--white {
    color: @white;
  }
  &--bgColor{
    &-green {
      background-color: @green;
    }
    &-blue {
      background-color: @blue;
    }
  }
}
</style>


