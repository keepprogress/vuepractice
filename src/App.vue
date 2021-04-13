<template>
  <div class="app">
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
                :class="{ active: current == 'personal info' }"
                aria-current="page"
                href="#"
                @click.prevent="current = 'personal info'"
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
        <Info />
        <Orders />
      </div>
    </div>
  </div>
</template>

<script>
import Info from './components/Info'
import Orders from './components/Orders'

export default {
  name: 'App',
  components: {
    Info,
    Orders
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
