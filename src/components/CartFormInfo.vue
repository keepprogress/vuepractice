<template>
  <div class="container">
    <div class="row">
      <div class="col-sm">
        <div class="form-group">
          <label for="FirstName">FirstName</label>
          <input
            type="text"
            class="form-control"
            id="FirstName"
            placeholder="Plz type your firstname"
            v-model="component_value.first_name"
          />
        </div>
      </div>
      <div class="col-sm">
        <div class="form-group">
          <label for="LastName">LastName</label>
          <input
            type="text"
            class="form-control"
            id="LastName"
            placeholder="Plz type your lastname"
            v-model="component_value.last_name"
          />
        </div>
      </div>
    </div>
    <div class="row">
      <div>
        <p class="ml-3">Gender</p>
      </div>
      <div class="col-sm text-left">
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="GenderRadio"
            id="Secret"
            value=0
            v-model="component_value.gender"
          />
          <label class="form-check-label" for="Secret"> Secret </label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="GenderRadio"
            id="Male"
            value=1
            v-model="component_value.gender"
          />
          <label class="form-check-label" for="Male"> Male </label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="GenderRadio"
            id="Female"
            value=2
            v-model="component_value.gender"
          />
          <label class="form-check-label" for="Female"> Female </label>
        </div>
      </div>
    </div>
    <div class="text-left">
      <label for="Address">Address</label>
      <input
        type="text"
        class="form-control"
        id="Address"
        placeholder="Plz type your Address"
        v-model="component_value.address"
        :disabled="this.component_value.is_homeless"
      />
    </div>
    <div class="pt-3">
      <div class="form-check text-left">
        <input
          class="form-check-input"
          type="checkbox"
          value=""
          id="flexCheckDefault"
          v-model="component_value.is_homeless"
          @input="deleteAddress"
        />
        <label class="form-check-label" for="flexCheckDefault">
          此客戶居無定所
        </label>
      </div>
    </div>
    <div class="pt-2 text-left">
      <p class="mb-2">Job</p>
      <select class="form-select" aria-label="Default select example" v-model="component_value.job">
        <option value=null>保密</option>
        <option value="agent">調查員</option>
        <option value="secret_agent">秘密調查員</option>
        <option value="agent_of_secret_agent">秘密調查員的調查員</option>
      </select>
    </div>
    <div class="text-left">
      <p class="mt-3">Note</p>
      <p>{{ countNoteStr }} / 2000 characters</p>
      <textarea
        class="form-control"
        aria-label="With textarea"
        placeholder="Note Here"
        v-model="component_value.note"
        maxlength="2000"
      ></textarea>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Info',
  props: {
    customerInfo: {
      type: Object,
      default: () => {}
    }
  },
  data () {
    return {
      note: ''
    }
  },
  computed: {
    countNoteStr () {
      if (!this.customerInfo.note) {
        return 0
      }
      const str = this.component_value.note
      return str.length
    },
    component_value () {
      return this.customerInfo
    }
  },
  methods: {
    deleteAddress () {
      this.component_value.address = ''
    }
  }
}
</script>
