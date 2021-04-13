<template>
    <div class="text-left">
        <h5>
            以下是某個人的訂單
        </h5>
        <ul>
            <li>{{ Orders.apple_count }}顆蘋果</li>
            <li>香蕉配料</li>
                <ul>
                    <li v-for="condiment in Orders.banana_condiments" v-bind:key="condiment">{{ condiment }}</li>
                </ul>
        </ul>

    </div>
</template>

<script>
export default {
  data () {
    return {
      Orders: {
        apple_count: 50,
        banana_condiments: ['chocolate', 'chili', 'garlic', 'soy_sauce']
      }
    }
  }

}
</script>

<style>

</style>
