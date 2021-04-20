<template>
  <div class="container">
    <div class="row">
      <div class="col-sm">
        <div class="form-group">
          <label for="FirstName">FirstName</label>
          <!-- because v-model contains v-on and v-bind:value so v-on:change="$emit('input', $event.target.value)" is not necesarry -->
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
        <h3 class="ml-3">gender</h3>
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
      <h6 class="mb-2">job</h6>
      <select class="form-select" aria-label="Default select example" v-model="component_value.job">
        <option value=null>保密</option>
        <option value="agent">調查員</option>
        <option value="secret_agent">秘密調查員</option>
        <option value="agent_of_secret_agent">秘密調查員的調查員</option>
      </select>
    </div>
    <div class="text-left">
      <h6 class="mt-3">Note</h6>
      <h6>{{ countStr }} / 2000 characters</h6>
      <textarea
        class="form-control"
        aria-label="With textarea"
        placeholder="Note Here"
        v-model="component_value.note"
      ></textarea>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Info',
  props: {
    childInfo: {
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
    countStr () {
      if (this.childInfo.note === null) {
        return 0
      }
      const str = this.component_value.note
      return str.trim().length
    },
    component_value () {
      return this.childInfo
    }
  },
  methods: {
    deleteAddress () {
      this.component_value.address = ''
    }
  }
}
</script>
