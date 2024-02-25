<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <div>
        <ul class="list-group">
            <li class="list-group-item" v-for="cartItem in cartItems" :key="cartItem.product.id">
                {{ cartItem.product.title }} - PLN {{ cartItem.product.price }} * {{ cartItem.quantity }}
                <button @click="$emit('remove-from-cart', cartItem.product)" class="btn badge badge-danger float-right">Remove from cart</button>
            </li>
        </ul>

        <div class="card p-3 my-5">
            <h4 class="text-center">PLN {{ formattedTotal }}</h4>
        </div>

        <button :disabled="cartItems.length === 0" @click="$emit('pay')" class="btn btn-info form-control">Pay Now</button>
    </div>
</template>

<script>
    export default {
        props: ['cartItems'],
        computed: {
            total() {
                return this.cartItems.reduce((acc, cartItem) => acc + cartItem.product.price * cartItem.quantity, 0)
            },
            formattedTotal() {
                return this.total.toFixed(2)
            }
        }
    }
</script>