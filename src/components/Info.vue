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
          />
        </div>
      </div>
    </div>
    <div class="row">
      <div calss="col-sm">
        <h6 class="ml-3">gender</h6>
      </div>
      <div calss="col-sm">
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="GenderRadio"
            id="Secret"
          />
          <label class="form-check-label" for="Secret"> Secret </label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="GenderRadio"
            id="Male"
            checked
          />
          <label class="form-check-label" for="Male"> Male </label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="GenderRadio"
            id="Female"
            checked
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
      />
    </div>
    <div class="pt-3">
      <div class="form-check text-left">
        <input
          class="form-check-input"
          type="checkbox"
          value=""
          id="flexCheckDefault"
        />
        <label class="form-check-label" for="flexCheckDefault">
          此客戶居無定所
        </label>
      </div>
    </div>
    <div class="pt-2 text-left">
      <h6 class="mb-2">job</h6>
      <select class="form-select" aria-label="Default select example">
        <option selected>保密</option>
        <option value="1">調查員</option>
        <option value="2">秘密調查員</option>
        <option value="3">秘密調查員的調查員</option>
      </select>
    </div>
    <div class="text-left">
      <h6 class="mt-3">Note</h6>
      <h7>{{ countStr }} / 2000 characters</h7>
      <textarea
        class="form-control"
        aria-label="With textarea"
        placeholder="Note Here"
        v-model="note"
      ></textarea>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Info',
  props: {
    TonsOfInfo: {
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
    countStr: function () {
      const str = this.$data.note
      return str.trim().length
    }
  }
}
</script>
