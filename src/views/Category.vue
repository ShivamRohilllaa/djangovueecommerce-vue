<template>
    <div class="page-category">
        <div class="columns is-multiline">
        <div class="columns is-12">
            <h2 class="is-size-2 has-text-centered">{{ category.name }}</h2>
        </div>
        <ProductBox 
        class="column is-3"
        v-for="product in category.products" 
        v-bind:key="product.id"
        v-bind:product="product" />
      </div>
        </div>
</template>
<script>
import axios from 'axios'
import ProductBox from '@/components/ProductBox'

export default {
    name: 'Category',
    components: {
        ProductBox
    },
    data() {
        return {
            category: {
                products: []
            }
        }
    },
    mounted() {
        this.getCategory()
    },
    watch: {
        $route(to, from) {
            if (to.name === 'Category') {
                this.getCategory()
            }
        }
    },
    methods: {
        async getCategory() {
            const categorySlug = this.$route.params.category_slug

            this.$store.commit('setIsLoading', true)

            axios
            .get(`api/products/${categorySlug}/`)
            .then( response => {
                this.category = response.data

                document.title = this.category.name + ' | Django Vue Ecommerce'

            })    
            .catch(error =>{
                console.log(error)
            })

            
            this.$store.commit('setIsLoading', false)
            
        }
    }
}
</script>