<template>
  <div class="container">
    <div>
    <h1>This is Order Component</h1>
    <h5>worldname is {{ worldname }}</h5>
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
        <input type="number" id="applenum" name="applenum" v-model="counter"
       min="1" max="10000">
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
        <input class="form-check-input" type="checkbox" id="inlineCheckbox1" value="chocolate">
        <label class="form-check-label" for="inlineCheckbox1">巧克力醬</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="checkbox" id="inlineCheckbox2" value="strawberry">
        <label class="form-check-label" for="inlineCheckbox2">草莓醬</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="checkbox" id="inlineCheckbox3" value="flax">
        <label class="form-check-label" for="inlineCheckbox3">胡麻醬</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="checkbox" id="inlineCheckbox4" value="miso">
        <label class="form-check-label" for="inlineCheckbox4">味噌</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="checkbox" id="inlineCheckbox5" value="chili">
        <label class="form-check-label" for="inlineCheckbox5">辣椒</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="checkbox" id="inlineCheckbox6" value="garlic">
        <label class="form-check-label" for="inlineCheckbox6">大蒜</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="checkbox" id="inlineCheckbox7" value="soy_sauce">
        <label class="form-check-label" for="inlineCheckbox7">醬油</label>
      </div>
    </div>
  </div>
</template>>

<script>
export default {
  props: {
    worldname: {
      type: String,
      default: '',
      required: false
    }
  },
  data () {
    return {
      counter: 1
    }
  },
  methods: {
    handlePlusOneClick () {
      this.$data.counter++
    },
    handleMinusOneClick () {
      if (this.$data.counter > 0) {
        this.$data.counter--
      }
    },
    handlePlusFiveClick () {
      this.$data.counter += 5
    },
    handleMinusFiveClick () {
      if (this.$data.counter > 4) {
        this.$data.counter -= 5
      }
    }
  }
}
</script>

<style>
</style>
