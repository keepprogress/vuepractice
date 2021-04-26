<template>
    <div class="text-left">
        <p>
            以下是{{ info_full_name }}的訂單
        </p>
        <ul>
            <li>{{ orders.apple_count }}顆蘋果</li>
            <li v-if="!bananaIsEmpty">香蕉配料</li>
            <ul>
              <li v-for="condiment in bananaCondimentView" :key="condiment">{{ condiment }}</li>
            </ul>
        </ul>
    </div>
</template>

<script>
export default {
  props: {
    orders: {
      type: Object,
      default: () => {},
    },
    customerInfo: {
      type: Object,
      default: () => {},
    },
  },
  data() {
    return {
      Orders: {
        apple_count: 50,
        banana_condiments: ['chocolate', 'chili', 'garlic', 'soy_sauce'],
      },
      tempOrder: {},
      compareBanana: {
        chocolate: '巧克力醬',
        strawberry: '草莓醬',
        flax: '胡麻醬',
        miso: '味噌',
        chili: '辣椒',
        garlic: '大蒜',
        soy_sauce: '醬油',
        thick_soy_sauce: '醬油膏',
        herbal_cream: '百草膏',
      },
      bananaIsEmpty: false,
      bananaCondimentView: [],
    };
  },
  computed: {
    // VisualMandarinCondiment () {
    //   const b = []
    //   for (let index = 0; index < this.$data.tempBanana.length; index++) {
    //     if (this.$data.compareBanana[this.$data.tempBanana[index]]) {
    //       b.push(this.$data.compareBanana[this.$data.tempBanana[index]])
    //     }
    //   }
    //   return b
    // },
    info_full_name() {
      if (!this.customerInfo.first_name.trim() && !this.customerInfo.last_name.trim()) {
        return 'unknown';
      } if (!this.customerInfo.first_name) {
        return this.customerInfo.last_name;
      } if (!this.customerInfo.last_name) {
        return this.customerInfo.first_name;
      }
      // return `${this.customerInfo.last_name} ${this.customerInfo.first_name}`;
      return [this.customerInfo.last_name, ' ', this.customerInfo.first_name].join('');
    },
  },
  watch: {
    orders: {
      handler() {
        const b = [];
        this.$data.tempBanana = this.orders.banana_condiments;
        if (!this.$data.tempBanana[0]) {
          this.$data.bananaIsEmpty = true;
        } else {
          this.$data.bananaIsEmpty = false;
        }
        for (let index = 0; index < this.$data.tempBanana.length; index += 1) {
          if (this.$data.compareBanana[this.$data.tempBanana[index]]) {
            b.push(this.$data.compareBanana[this.$data.tempBanana[index]]);
          }
        }
        this.$data.bananaCondimentView = b;
      },
      deep: true,
      immediate: true,
    },
  },
};
</script>

<style>

</style>
