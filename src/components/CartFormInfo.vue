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
            v-model="computed_customerInfo.first_name"
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
            v-model="computed_customerInfo.last_name"
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
            value="0"
            v-model="computed_customerInfo.gender"
          />
          <label class="form-check-label" for="Secret"> Secret </label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="GenderRadio"
            id="Male"
            value="1"
            v-model="computed_customerInfo.gender"
          />
          <label class="form-check-label" for="Male"> Male </label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="GenderRadio"
            id="Female"
            value="2"
            v-model="computed_customerInfo.gender"
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
        v-model="computed_customerInfo.address"
        :disabled="this.computed_customerInfo.is_homeless"
      />
    </div>
    <div class="pt-3">
      <div class="form-check text-left">
        <input
          class="form-check-input"
          type="checkbox"
          value=""
          id="flexCheckDefault"
          v-model="computed_customerInfo.is_homeless"
          @input="deleteAddress"
        />
        <label class="form-check-label" for="flexCheckDefault">
          此客戶居無定所
        </label>
      </div>
    </div>
    <div class="pt-2 text-left">
      <p class="mb-2">Job</p>
      <select
        class="form-select"
        aria-label="Default select example"
        v-model="computed_customerInfo.job"
      >
        <option value="null">保密</option>
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
        v-model="computed_customerInfo.note"
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
      default: () => {},
    },
  },
  data() {
    return {
      note: '',
    };
  },
  computed: {
    countNoteStr() {
      if (!this.customerInfo.note) {
        return 0;
      }
      const str = this.computed_customerInfo.note;
      return str.length;
    },
    computed_customerInfo() {
      return this.customerInfo;
    },
  },
  methods: {
    deleteAddress() {
      this.computed_customerInfo.address = '';
    },
  },
};
</script>
