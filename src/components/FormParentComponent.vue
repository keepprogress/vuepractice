<template>
  <div class="parent">
    <div class="container">
      <h5>Form A0000001</h5>
      <h5>跳至, 共5張</h5>
      <div class="p-2 col-sm">
        <button type="button" class="btn btn-primary">Log this Form</button>
        <button type="button" class="btn btn-info">Log all forms</button>
        <button type="button" class="btn btn-danger">Delete this form</button>
      </div>
      <div class="container">
        <div class="mb-3">
          <ul class="nav nav-tabs">
            <li class="nav-item">
              <a
                class="nav-link"
                :class="{ active: current == 'Info' }"
                aria-current="page"
                href="#"
                @click.prevent="current = 'Info'"
                >Personal Info</a
              >
            </li>
            <li class="nav-item">
              <a
                class="nav-link"
                :class="{ active: current == 'Orders' }"
                href="#"
                @click.prevent="current = 'Orders'"
                >Orders</a
              >
            </li>
            <li class="nav-item">
              <a
                class="nav-link"
                :class="{ active: current == 'Overview' }"
                href="#"
                @click.prevent="current = 'Overview'"
                >Overview</a
              >
            </li>
          </ul>
        </div>
        <keep-alive>
          <Info v-if="current === 'Info'" :childInfo="infoAndOrder.personal_info"/>
        </keep-alive>
        <keep-alive>
          <Orders v-if="current === 'Orders'" :orders="infoAndOrder.orders" v-on:handlePlusOneClick="incrementParent"/>
        </keep-alive>
        <keep-alive>
          <Overview v-if="current === 'Overview'" />
        </keep-alive>
        <div>Here is parent component Apple count {{ this.$data.infoAndOrder.orders.apple_count }}</div>
        <div class="col">
          <button type="button" @click="incrementParent" class="btn btn-light">+1</button>
        </div>
        <!-- <keep-alive>
          <component :is="current"></component>
        </keep-alive> -->
      </div>
    </div>
  </div>
</template>

<script>
import Info from '@/components/Info.vue'
import Orders from '@/components/Orders.vue'
import Overview from '@/components/Overview.vue'

export default {
  name: 'App',
  components: {
    Info,
    Orders,
    Overview
  },
  data () {
    return {
      snowworld: 'newwwwwww world',
      current: 'Info',
      strLength: 0,
      infoAndOrder: {
        id: 'A0000001',
        personal_info: {
          first_name: 'Fishman',
          last_name: 'ILike',
          gender: 1,
          address: 'ABCDEFG',
          is_homeless: false,
          job: null,
          note: null
        },
        orders: {
          apple_count: 20,
          banana_condiments: ['chocolate', 'chili', 'garlic', 'soy_sauce']
        }
      }
    }
  },
  methods: {
    incrementParent: function () {
      this.$data.infoAndOrder.orders.apple_count++
    }
  }
}
</script>

<style>
#parent {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
