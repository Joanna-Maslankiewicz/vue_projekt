<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <div class="card my-5">
        <div class="card-body text-center">
            <h5 class="text-center card-title">{{ product.title }}</h5>
            <img :src="product.image" :alt="product.title" class="product-image img-fluid mb-3 mx-auto" />
            <p class="text-center text-muted card-text display-4">PLN {{ Number(product.price).toFixed() }}</p>
            
            <div class="text-center">
                <button @click="decrementQuantity" class="btn btn-secondary mx-2">-</button>
                <span class="mx-2">{{ quantity }}</span>
                <button @click="incrementQuantity" class="btn btn-secondary mx-2">+</button>
            </div>

            <button :disabled="isInCart" @click="addToCart" class="btn btn-primary form-control mt-2">
                {{ isInCart ? 'Added to cart.' : 'Add to Cart' }}
            </button>
        </div>
    </div>
</template>

<script>
export default {
    props: ['product', 'isInCart'],
    data() {
        return {
            quantity: 1
        }
    },
    methods: {
        incrementQuantity() {
            this.quantity++
        },
        decrementQuantity() {
            if (this.quantity > 1) {
                this.quantity--
            }
        },
        addToCart() {
            this.$emit('add-to-cart', { product: this.product, quantity: this.quantity })
        }
    }
}
</script>

<style scoped>
.product-image {
    width: auto;
    height: 150px;
}
</style>