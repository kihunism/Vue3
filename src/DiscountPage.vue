<template>
    <div class="discount">
      <h4>{{ content }}</h4>
    </div>
</template>

<script>
export default {
    name: 'DiscountPage',
    data() {
        return {
            content: `지금 결제하면 ${this.discount}% 할인`,
            discount: 30
        }
    },
    methods: {
        
    },
}
</script>

<style>

</style>