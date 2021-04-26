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
      @handleOrderAppleInput="handleOrderAndInput"
      @PlusOneParent="PlusOneParent"
      @MinusOneParent="MinusOneParent"
      @PlusFiveParent="PlusFiveParent"
      @MinusFiveParent="MinusFiveParent"
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
import CartForm from './components/CartForm.vue';

export default {
  name: 'App',
  components: {
    CartForm,
  },
  data() {
    return {
      infoAndOrderArray: [
        {
          id: 'A0000003',
          personal_info: {
            first_name: 'Painter',
            last_name: null,
            gender: 0,
            address: null,
            is_homeless: true,
            job: 'agent_of_secret_agent',
            note: 'Strange',
          },
          orders: {
            apple_count: 1,
            banana_condiments: ['herbal_cream'],
          },
        },
        {
          id: 'A0000001',
          personal_info: {
            first_name: 'Fishman',
            last_name: 'ILike',
            gender: 1,
            address: 'ABCDEFG',
            is_homeless: false,
            job: null,
            note: null,
          },
          orders: {
            apple_count: 1,
            banana_condiments: ['chocolate', 'chili', 'garlic', 'soy_sauce'],
          },
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
            note: 'Hello, world',
          },
          orders: {
            apple_count: 15,
            banana_condiments: [],
          },
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
            note: '胡椒博士現身',
          },
          orders: {
            apple_count: 5,
            banana_condiments: ['chili', 'garlic'],
          },
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
            note: 'He is the president!',
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
              'thick_soy_sauce',
            ],
          },
        },
      ],
      currentPageNumber: 1,
      pages: [],
      totalId: [],
      nextPage: {
        index: '1',
        id: 'A0000001',
      },
      previousPage: {
        index: '',
        id: '',
      },
      infoAndOrderIsEmpty: false,
    };
  },
  computed: {
    singleForm() {
      return (
        this.$data.infoAndOrderArray[this.currentPageNumber - 1] || {
          id: '',
          personal_info: {
            first_name: '',
            last_name: '',
            gender: 0,
            address: '',
            is_homeless: false,
            job: null,
            note: '',
          },
          orders: {
            apple_count: 0,
            banana_condiments: [],
          },
        }
      );
    },
  },
  watch: {
    currentPageNumber: {
      handler() {
        for (
          let index = 0;
          index < this.$data.infoAndOrderArray.length;
          index += 1
        ) {
          if (this.$data.currentPageNumber === index + 1) {
            if (this.$data.currentPageNumber === this.$data.infoAndOrderArray.length) {
              this.$data.nextPage.id = '';
              this.$data.nextPage.index = '';
              this.$data.previousPage.index = index - 1;
              this.$data.previousPage.id = this.$data.infoAndOrderArray[
                index - 1
              ].id;
              return;
            }
            if (this.$data.currentPageNumber === 1) {
              this.previousPage.id = '';
              this.previousPage.index = '';
              this.$data.nextPage.index = index + 1;
              this.$data.nextPage.id = this.$data.infoAndOrderArray[index + 1].id;
              return;
            }
            this.$data.nextPage.index = index + 1;
            this.$data.nextPage.id = this.$data.infoAndOrderArray[index + 1].id;
            this.$data.previousPage.index = index - 1;
            this.$data.previousPage.id = this.$data.infoAndOrderArray[
              index - 1
            ].id;
          }
        }
      },
      deep: true,
      immediate: true,
    },
    infoAndOrderArray: {
      handler() {
        if (this.$data.infoAndOrderArray[0]) {
          this.$data.infoAndOrderIsEmpty = false;
        } else {
          this.$data.infoAndOrderIsEmpty = true;
        }
        this.setPages();
      },
      deep: true,
      immediate: true,
    },
  },
  methods: {
    setPages() {
      this.$data.totalId = [];
      this.$data.pages = [];
      for (let index = 1; index <= this.infoAndOrderArray.length; index += 1) {
        this.$data.pages.push(index);
      }
      for (let i = 0; i < this.$data.infoAndOrderArray.length; i += 1) {
        this.$data.totalId.push(this.$data.infoAndOrderArray[i].id);
      }
    },
    hanldleCurentPageIncrement() {
      if (this.$data.currentPageNumber < this.$data.pages.length) {
        this.$data.currentPageNumber += 1;
      }
    },
    hanldleCurentPagedecrease() {
      if (this.$data.currentPageNumber > 1) {
        this.$data.currentPageNumber -= 1;
      }
    },
    handleLogSingleForm() {
      console.log(this.$data.infoAndOrderArray[this.currentPageNumber - 1]);
    },
    handleLogAllForm() {
      console.log(this.$data.infoAndOrderArray);
    },
    handleDeleteSingleForm() {
      const arr = this.$data.infoAndOrderArray;
      if (arr.length > 0) {
        const singleFormTemp = this.singleForm.id;
        for (let index = 0; index < arr.length; index += 1) {
          if (singleFormTemp === arr[index].id) {
            this.$data.infoAndOrderArray.splice(index, 1);
            this.$data.currentPageNumber = 1;
          }
        }
      }
    },
    handleSwitchPageDownside(idSingle) {
      const arr = this.$data.infoAndOrderArray;
      let foundedId = 0;
      for (let index = 0; index < arr.length; index += 1) {
        if (arr[index].id === idSingle) {
          foundedId = index;
        }
      }
      this.$data.currentPageNumber = foundedId + 1;
    },
    handleParentSwitchPage(e) {
      const arr = this.$data.infoAndOrderArray;
      let foundedId = 0;
      for (let index = 0; index < arr.length; index += 1) {
        if (arr[index].id === e.target.value) {
          foundedId = index;
        }
      }
      this.$data.currentPageNumber = foundedId + 1;
    },
    PlusOneParent() {
      if (this.singleForm.orders.apple_count < 100) {
        this.singleForm.orders.apple_count += 1;
      }
    },
    MinusOneParent() {
      if (this.singleForm.orders.apple_count > 1) {
        this.singleForm.orders.apple_count -= 1;
      }
    },
    PlusFiveParent() {
      if (this.singleForm.orders.apple_count < 96) {
        this.singleForm.orders.apple_count += 5;
      }
    },
    MinusFiveParent() {
      if (this.singleForm.orders.apple_count > 5) {
        this.singleForm.orders.apple_count -= 5;
      }
    },
    handleOrderAndInput(e) {
      this.singleForm.orders.apple_count = Math.round(e.target.value);
    },
  },
};
</script>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
