<template>
  <div class="app">
    <form-parent-component
    :personalInfo="singleForm.personal_info"
    :order="singleForm.orders"
    :id="singleForm.id"
    :totalPages="pages"
    :totalId="totalId"
    @FormTopIDChangeHandler="handleParentSwitchPage"
    />
  </div>
  <div>
    <nav aria-label="Page navigation example">
      <ul class="pagination justify-content-center">
        <li class="page-item">
          <button type="button" class="page-link" @click="hanldleCurentPagedecrease">Previous</button>
        </li>
        <li class="page-item" v-for="page in pages" v-bind:key="page">
          <button type="button" class="page-link" @click="this.currentPage = page"> {{ page }}</button>
        </li>
        <li class="page-item">
          <button type="button" class="page-link" @click="hanldleCurentPageIncrement">Next</button>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
import FormParentComponent from './components/FormParentComponent.vue'

export default {
  name: 'App',
  components: {
    FormParentComponent
  },
  data () {
    return {
      infoAndOrderArray: [
        {
          id: 'A0000001',
          personal_info:
            {
              first_name: 'Fishman',
              last_name: 'ILike',
              gender: 1,
              address: 'ABCDEFG',
              is_homeless: false,
              job: null,
              note: null
            },
          orders: {
            apple_count: 1,
            banana_condiments: ['chocolate', 'chili', 'garlic', 'soy_sauce']
          }
        },
        {
          id: 'A0000002',
          personal_info: {
            first_name: null,
            last_name: 'Somebody',
            gender: 2,
            address: 'QWERTY',
            is_homeless: false,
            job: 'secret_agent',
            note: 'Hello, world'
          },
          orders: {
            apple_count: 15,
            banana_condiments: []
          }
        },
        {
          id: 'A0000003',
          personal_info: {
            first_name: 'Painter',
            last_name: null,
            gender: 0,
            address: null,
            is_homeless: true,
            job: 'agent_of_secret_agent',
            note: 'Strange'
          },
          orders: {
            apple_count: 1,
            banana_condiments: ['herbal_cream']
          }
        },
        {
          id: 'A0000004',
          personal_info: {
            first_name: 'President',
            last_name: 'Mr.',
            gender: 1,
            address: 'America',
            is_homeless: false,
            job: 'secret_agent',
            note: 'He is the president!'
          },
          orders: {
            apple_count: 100,
            banana_condiments: ['chocolate', 'strawberry', 'flax', 'miso', 'chili', 'garlic', 'soy_sauce', 'thick_soy_sauce']
          }
        },
        {
          id: 'A0000005',
          personal_info: {
            first_name: 'Pepper',
            last_name: 'Dr.',
            gender: 0,
            address: 'Farm',
            is_homeless: false,
            job: 'agent',
            note: '胡椒博士現身'
          },
          orders: {
            apple_count: 5,
            banana_condiments: ['chili', 'garlic']
          }
        }
      ],
      currentPage: 1,
      pages: [],
      totalId: []
    }
  },
  methods: {
    setPages () {
      for (let index = 1; index <= this.infoAndOrderArray.length; index++) {
        this.pages.push(index)
      }
    },
    hanldleCurentPageIncrement () {
      if (this.$data.currentPage < this.$data.pages.length) {
        this.$data.currentPage++
      }
    },
    hanldleCurentPagedecrease () {
      if (this.$data.currentPage > 1) {
        this.$data.currentPage--
      }
    },
    handleParentSwitchPage (e) {
      console.log(e.target.value)
      const arr = this.$data.infoAndOrderArray
      let foundedId = 0
      for (let index = 0; index < arr.length; index++) {
        if (arr[index].id === e.target.value) {
          console.log('we found ' + arr[index].id)
          foundedId = index
        }
      }
      console.log(foundedId)
      this.$data.currentPage = foundedId + 1
    }
  },
  // use computed to dynamic switch props
  computed: {
    singleForm () {
      return this.$data.infoAndOrderArray[this.currentPage - 1]
    }
  },
  // assume that JSON data would just send once so put setPage in created() <<= would run once when this component be started
  created () {
    this.setPages()
    console.log(this.$data.infoAndOrderArray[this.currentPage - 1])
    for (let i = 0; i < this.$data.infoAndOrderArray.length; i++) {
      this.$data.totalId.push(this.$data.infoAndOrderArray[i].id)
    }
    console.log(this.$data.totalId)
    console.log(this.pages)
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
