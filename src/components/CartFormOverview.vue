<template>
    <div class="text-left">
        <h5>
            以下是{{ info_full_name }}的訂單
        </h5>
        <ul>
            <li>{{ orders.apple_count }}顆蘋果</li>
            <li v-if="bananaIsEmpty">香蕉配料</li>
                <ul>
                    <li v-for="condiment in VisualMandarinCondiment" :key="condiment">{{ condiment }}</li>
                </ul>
        </ul>
    </div>
</template>

<script>
export default {
  data () {
    return {
      Orders: {
        apple_count: 50,
        banana_condiments: ['chocolate', 'chili', 'garlic', 'soy_sauce']
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
        herbal_cream: '百草膏'
      },
      bananaIsEmpty: false
    }
  },
  props: {
    orders: {
      type: Object,
      default: () => {}
    },
    childInfo: {
      type: Object,
      default: () => {}
    }
  },
  computed: {
    VisualMandarinCondiment () {
      const b = []
      for (let index = 0; index < this.$data.tempBanana.length; index++) {
        if (this.$data.compareBanana[this.$data.tempBanana[index]]) {
          b.push(this.$data.compareBanana[this.$data.tempBanana[index]])
        }
      }
      console.log(b)
      return b
    },
    info_full_name () {
      if (!this.childInfo.first_name & !this.childInfo.last_name) {
        return 'unknown'
      } else {
        return this.childInfo.last_name + ' ' + this.childInfo.first_name
      }
    }
  },
  watch: {
    orders: {
      handler () {
        this.$data.tempBanana = this.orders.banana_condiments
        console.log('receive prop to $data')
        console.log(this.$data.tempBanana)
        if (!this.$data.tempBanana) {
          this.$data.bananaIsEmpty = true
        } else {
          this.$data.bananaIsEmpty = false
        }
      },
      deep: true,
      immediate: true
    }
  }
}
</script>

<style>

</style>
