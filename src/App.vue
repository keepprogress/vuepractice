<template>
  <div class="app">
    <CartForm
      :personalInfo="singleForm.personal_info"
      :order="singleForm.orders"
      :id="singleForm.id"
      :totalPages="pages"
      :totalId="totalId"
      :nextPage="nextPage"
      :previousPage="previousPage"
      :infoAndOrderIsEmpty="infoAndOrderIsEmpty"
      @FormTopIDChangeHandler="handleParentSwitchPage"
      @LogSingleFormHandler="handleLogSingleForm"
      @LogAllFormHandler="handleLogAllForm"
      @DeleteSingleFormHandler="handleDeleteSingleForm"
      @hanldleCurentPagedecrease="hanldleCurentPagedecrease"
      @hanldleCurentPageIncrement="hanldleCurentPageIncrement"
      @handleSwitchPageDownside="handleSwitchPageDownside"
    />
  </div>
</template>

<script>
import CartForm from './components/CartForm.vue'

export default {
  name: 'App',
  components: {
    CartForm
  },
  data () {
    return {
      infoAndOrderArray: [
        {
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
            banana_condiments: [
              'chocolate',
              'strawberry',
              'flax',
              'miso',
              'chili',
              'garlic',
              'soy_sauce',
              'thick_soy_sauce'
            ]
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
      totalId: [],
      nextPage: {
        index: '1',
        id: 'A0000002'
      },
      previousPage: {
        index: '',
        id: ''
      },
      infoAndOrderIsEmpty: false
    }
  },
  // use computed to dynamic switch props
  computed: {
    singleForm () {
      return (
        this.$data.infoAndOrderArray[this.currentPage - 1] || {
          id: '',
          personal_info: {
            first_name: '',
            last_name: '',
            gender: 0,
            address: '',
            is_homeless: false,
            job: null,
            note: ''
          },
          orders: {
            apple_count: 0,
            banana_condiments: []
          }
        }
      )
    }
  },
  watch: {
    currentPage () {
      for (let index = 0; index < this.$data.infoAndOrderArray.length; index++) {
        if (this.$data.currentPage === index + 1) {
          if (this.$data.currentPage === this.$data.infoAndOrderArray.length) {
            this.$data.nextPage.id = ''
            this.$data.nextPage.index = ''
            this.$data.previousPage.index = index - 1
            this.$data.previousPage.id = this.$data.infoAndOrderArray[index - 1].id
            console.log(this.previousPage)
            console.log(this.$data.nextPage)
            return
          }
          if (this.$data.currentPage === 1) {
            this.previousPage.id = ''
            this.previousPage.index = ''
            this.$data.nextPage.index = index + 1
            this.$data.nextPage.id = this.$data.infoAndOrderArray[index + 1].id
            console.log(this.previousPage)
            console.log(this.$data.nextPage)
            return
          }
          console.log('we found next page in watch: ' + index)
          this.$data.nextPage.index = index + 1
          this.$data.nextPage.id = this.$data.infoAndOrderArray[index + 1].id
          console.log(this.$data.nextPage)
          this.$data.previousPage.index = index - 1
          this.$data.previousPage.id = this.$data.infoAndOrderArray[index - 1].id
          console.log(this.$data.previousPage)
        }
      }
    },
    // when you watch an array or an object, Vue has no idea that you've changed what's inside that prop.
    // You have to tell Vue that you want it to inspect inside of the prop when watching for changes.
    // see https://michaelnthiessen.com/how-to-watch-nested-data-vue/
    infoAndOrderArray: {
      handler () {
        console.log('infoAndOrderArray changed')
        if (this.$data.infoAndOrderArray[0]) {
          this.$data.infoAndOrderIsEmpty = false
        } else {
          this.$data.infoAndOrderIsEmpty = true
        }
        this.setPages()
      },
      deep: true,
      immediate: true
    }
  },
  methods: {
    setPages () {
      this.$data.totalId = []
      this.$data.pages = []
      for (let index = 1; index <= this.infoAndOrderArray.length; index++) {
        this.$data.pages.push(index)
      }
      console.log(this.$data.infoAndOrderArray[this.currentPage - 1])
      for (let i = 0; i < this.$data.infoAndOrderArray.length; i++) {
        this.$data.totalId.push(this.$data.infoAndOrderArray[i].id)
      }
      console.log(this.$data.totalId)
      console.log(this.$data.pages)
      console.log(this.setPages)
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
    handleLogSingleForm () {
      console.log(this.$data.infoAndOrderArray[this.currentPage - 1])
    },
    handleLogAllForm () {
      console.log(this.$data.infoAndOrderArray)
    },
    handleDeleteSingleForm () {
      const arr = this.$data.infoAndOrderArray
      if (arr.length === 0) {
        console.log('we have no customer!!')
      }
      if (arr.length > 0) {
        console.log(this.singleForm.id)
        const singleFormTemp = this.singleForm.id
        for (let index = 0; index < arr.length; index++) {
          if (singleFormTemp === arr[index].id) {
            console.log('we found item to delete' + arr[index].id)
            this.$data.infoAndOrderArray.splice(index, 1)
            this.$data.currentPage = 1
            console.log(this.$data.infoAndOrderArray)
          }
        }
      }
      console.log(this.$data.infoAndOrderArray[this.currentPage - 1])
    },
    handleSwitchPageDownside (e) {
      console.log(e)
      const arr = this.$data.infoAndOrderArray
      let foundedId = 0
      for (let index = 0; index < arr.length; index++) {
        if (arr[index].id === e) {
          console.log('we found ' + arr[index].id)
          foundedId = index
        }
      }
      console.log(foundedId)
      this.$data.currentPage = foundedId + 1
    },
    // which page to change depending on currentPage so handleParentSwitchPage will find index in this.$data.infoAndOrderArray
    // and send it to foundedId if the selected id value is matched with this.$data.infoAndOrderArray
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
  }
  // assume that JSON data would just send once so put setPage in created() <<= would run once when this component be started
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
