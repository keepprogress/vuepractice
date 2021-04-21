<template>
  <div class="container">
    <div>
    <h1>This is Order Component</h1>
    <!-- <h5>worldname is {{ worldname }}</h5> -->
  </div>
    <div class="row align-right">
      <div class="col">
        <h5 class="text-left">Apple</h5>
      </div>
      <div class="col">
        <button type="button" @click="handlePlusFiveClick" class="btn btn-light">+5</button>
      </div>
      <div class="col">
        <button type="button" @click="handlePlusOneClick" class="btn btn-light">+1</button>
      </div>
      <div class="col">
        <input type="number" id="applenum" name="applenum" :value="orders.apple_count" @change="handleOrderAppleInput"
       min="1" max="100">
      </div>
      <div class="col">
        <button type="button" @click="handleMinusOneClick" class="btn btn-light">-1</button>
      </div>
      <div class="col">
        <button type="button" @click="handleMinusFiveClick" class="btn btn-light">-5</button>
      </div>
    </div>
    <div class="row">
      <h5>Banana</h5>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="checkbox" id="inlineCheckbox1" value="chocolate" v-model="Orders.banana_condiments">
        <label class="form-check-label" for="inlineCheckbox1">巧克力醬</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="checkbox" id="inlineCheckbox2" value="strawberry" v-model="Orders.banana_condiments">
        <label class="form-check-label" for="inlineCheckbox2">草莓醬</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="checkbox" id="inlineCheckbox3" value="flax" v-model="Orders.banana_condiments">
        <label class="form-check-label" for="inlineCheckbox3">胡麻醬</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="checkbox" id="inlineCheckbox4" value="miso" v-model="Orders.banana_condiments">
        <label class="form-check-label" for="inlineCheckbox4">味噌</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="checkbox" id="inlineCheckbox5" value="chili" v-model="Orders.banana_condiments">
        <label class="form-check-label" for="inlineCheckbox5">辣椒</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="checkbox" id="inlineCheckbox6" value="garlic" v-model="Orders.banana_condiments">
        <label class="form-check-label" for="inlineCheckbox6">大蒜</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="checkbox" id="inlineCheckbox7" value="soy_sauce" v-model="Orders.banana_condiments">
        <label class="form-check-label" for="inlineCheckbox7">醬油</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="checkbox" id="inlineCheckbox8" value="thick_soy_sauce" v-model="Orders.banana_condiments">
        <label class="form-check-label" for="inlineCheckbox8">醬油膏</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="checkbox" id="inlineCheckbox9" value="herbal_cream" v-model="Orders.banana_condiments">
        <label class="form-check-label" for="inlineCheckbox9">百草膏</label>
      </div>
    </div>
  </div>
</template>>

<script>
export default {
  props: {
    orders: {
      type: Object,
      default: () => {},
      required: false
    }
  },
  data () {
    return {
      counter: 1,
      testCheckBox: ['chocolate', 'garlic']
    }
  },
  computed: {
    Orders () {
      return this.orders
    }
  },
  methods: {
    handlePlusOneClick () {
      this.$emit('handle-plus-one-click')
    },
    handleMinusOneClick () {
      this.$emit('handle-minus-one-click')
    },
    handlePlusFiveClick () {
      this.$emit('handle-plus-five-click')
    },
    handleMinusFiveClick () {
      this.$emit('handle-minus-five-click')
    },
    handleOrderAppleInput (e) {
      this.$emit('handle-order-apple-input', e)
    }
  }
}

</script>

<style>
</style>
