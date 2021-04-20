<template>
  <div class="parent">
    <div class="container">
      <h1>Form {{ id }}</h1>
      <h2>跳至,
        <!-- use v-bind to oneWay Binding value in 'id' props -->
        <select class="form-select" aria-label="Default select example" @change="FormTopIDChangeHandler">
          <option v-for="idSingle in totalId" :key="idSingle">{{ idSingle }}</option>
        </select>共{{ totalPages.length }}張</h2>
        {{ totalId }}
      <div class="p-2 col-sm">
        <button type="button" class="btn btn-primary" @click="LogSingleFormHandler">Log this Form</button>
        <button type="button" class="btn btn-info" @click="LogAllFormHandler">Log all forms</button>
        <button type="button" class="btn btn-danger" @click="DeleteSingleFormHandler">Delete this form</button>
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
          <CartFormInfo
          v-if="current === 'Info'"
          :childInfo="this.$data.infoAndOrder.personal_info"
          />
        </keep-alive>
        <keep-alive>
          <CartFormOrders
          v-if="current === 'Orders'"
          :orders="this.$data.infoAndOrder.orders"
          @handlePlusOneClick="PlusOneParent"
          @handleMinusOneClick="MinusOneParent"
          @handlePlusFiveClick="PlusFiveParent"
          @handleMinusFiveClick="MinusFiveParent"
          />
        </keep-alive>
        <keep-alive>
          <CartFormOverview v-if="current === 'Overview'"
          :orders="this.$data.infoAndOrder.orders"/>
        </keep-alive>
        <div>Here is parent component firstname {{ this.$data.infoAndOrder.personal_info.first_name }}</div>
        <div>Here is parent component lastname {{ this.$data.infoAndOrder.personal_info.last_name }}</div>
        <div>Here is parent component gender {{ this.$data.infoAndOrder.personal_info.gender }}</div>
        <div>Here is parent component Address {{ this.$data.infoAndOrder.personal_info.address }}</div>
        <div>Here is parent component Job {{ this.$data.infoAndOrder.personal_info.job }}</div>
        <div>Here is parent component note {{ this.$data.infoAndOrder.personal_info.note }}</div>
        <div>Here is parent component Apple count {{ this.$data.infoAndOrder.orders.apple_count }}</div>
        <div>Here is parent component Banana Condiments {{ this.$data.infoAndOrder.orders.banana_condiments }}</div>
        <div class="col">
          <button type="button" @click="PlusOneParent" class="btn btn-light">+1</button>
        </div>
        <div>{{ this.order }}</div>
        <div>
      <nav aria-label="Page navigation example">
        <ul class="pagination justify-content-center">
          <li class="page-item">
            <button
              type="button"
              class="page-link"
              data-toggle="tooltip"
              data-placement="right"
              :title= previousPage.id
              @click="hanldleCurentPagedecrease"
            >
              Previous
            </button>
          </li>
          <li class="page-item" v-for="idSingle in totalId" :key="idSingle">
            <button
              type="button"
              class="page-link"
              data-toggle="tooltip"
              data-placement="right"
              :title= idSingle
              @click="$emit('handleSwitchPageDownside', idSingle)"
            >
              {{ totalId.indexOf(idSingle) + 1 }}
            </button>
          </li>
          <li class="page-item">
            <button
              type="button"
              class="page-link"
              data-toggle="tooltip"
              data-placement="right"
              :title= nextPage.id
              @click="hanldleCurentPageIncrement"
            >
              Next
            </button>
          </li>
        </ul>
      </nav>
    </div>
        <!-- <keep-alive>
          <component :is="current"></component>
        </keep-alive> -->
      </div>
    </div>
  </div>
</template>

<script>
import CartFormInfo from '@/components/CartFormInfo.vue'
import CartFormOrders from '@/components/CartFormOrders.vue'
import CartFormOverview from '@/components/CartFormOverview.vue'

export default {
  name: 'com1',
  components: {
    CartFormInfo,
    CartFormOrders,
    CartFormOverview
  },
  props: {
    order: {
      type: Object,
      default: () => {}
    },
    personalInfo: {
      type: Object,
      default: () => {}
    },
    id: {
      type: String
    },
    totalPages: {
      type: Array
    },
    totalId: {
      type: Array
    },
    previousPage: {
      type: Object,
      default: () => {}
    },
    nextPage: {
      type: Object,
      default: () => {}
    }
  },
  data () {
    return {
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
    PlusOneParent: function () {
      if (this.$data.infoAndOrder.orders.apple_count < 10000) {
        this.$data.infoAndOrder.orders.apple_count++
      }
    },
    MinusOneParent: function () {
      if (this.$data.infoAndOrder.orders.apple_count > 0) {
        this.$data.infoAndOrder.orders.apple_count--
      }
    },
    PlusFiveParent: function () {
      if (this.$data.infoAndOrder.orders.apple_count < 9995) {
        this.$data.infoAndOrder.orders.apple_count += 5
      }
    },
    MinusFiveParent () {
      if (this.$data.infoAndOrder.orders.apple_count > 4) {
        this.$data.infoAndOrder.orders.apple_count -= 5
      }
    },
    FormTopIDChangeHandler (e) {
      this.$emit('FormTopIDChangeHandler', (e))
    },
    LogSingleFormHandler () {
      this.$emit('LogSingleFormHandler')
    },
    LogAllFormHandler () {
      this.$emit('LogAllFormHandler')
    },
    DeleteSingleFormHandler () {
      this.$emit('DeleteSingleFormHandler')
    },
    hanldleCurentPagedecrease () {
      this.$emit('hanldleCurentPagedecrease')
    },
    hanldleCurentPageIncrement () {
      this.$emit('hanldleCurentPageIncrement')
    }
  },
  watch: {
    personalInfo () {
      this.$data.infoAndOrder.personal_info = this.personalInfo
    },
    order () {
      this.$data.infoAndOrder.orders = this.order
    },
    id () {
      this.$data.id = this.id
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
