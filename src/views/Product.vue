<template>
    <div class="page-product has-text-center">
        <div class="columns is-multiline">
            <div class="column is-9 ">
                <figure>
                    <img v-bind:src="product.get_image" alt="">
                </figure>
                <h1 class="title has-text-white">{{ product.name }}</h1>

                <p class="subtitle has-text-white"> {{ product.description }} </p> 
            </div>
            <div class="column is-3 ">
                <h2 class="subtitle has-text-white">Info:</h2>

                <p><strong class="has-text-white">Price: R$ {{ product.price }}</strong></p>

                <div class="field has-addons mt-6">
                    <div class="control">
                        <input type="number" class="input" min="1" v-model="quantity">
                    </div>
                    
                    <div class="control">
                        <a class="button is-success is-focused" @click="addToCart">Add to cart</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { toast } from 'bulma-toast'
import axios from 'axios'

export default {
    name: 'Product',
    data() {
        return {
            product: {},
            quantity: 1
        }
    },
    mounted(){
        this.getProduct()
    },
    methods: {
        getProduct() {
            const category_slug = this.$route.params.category_slug
            const product_slug = this.$route.params.product_slug
            
            axios
                .get(`/api/v1/products/${category_slug}/${product_slug}`)
                .then(response => {
                    this.product = response.data

                    document.title = this.product.name + ' | DMarT'
                })
                .catch(error =>{
                    console.log(error)
                })
        },
        addToCart() {
            if (isNaN(this.quantity) || this.quantity < 1) {
                this.quantity = 1
            }
            
            const item = {
                product: this.product,
                quantity: this.quantity
            }

            this.$store.commit('addToCart', item)

            toast({
                message: 'The product was added to your cart',
                type: 'is-success',
                dismissible: true,
                pauseOnHover: true,
                duration: 2000,
                position: 'bottom-right',
            })
        }
    }
}
</script>