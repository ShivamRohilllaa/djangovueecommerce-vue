<template>
<div id="wrapper">
<nav class="navbar is-dark">
<div class="navbar-brand">
<router-link to="/" class="navbar-item">
<strong> Django Vue Ecommerce </strong>
</router-link>

<a class="navbar-burger" aria-label="menu" aria-expanded="false" data-target="navbar-menu" @click="showMobileMenu = !showMobileMenu">
<span aria-hidden="true"></span>
<span aria-hidden="true"></span>
<span aria-hidden="true"></span>
</a>  
</div>
<div class="navbar-menu" id="navbar-menu" v-bind:class="{'is-active':showMobileMenu}">
<div class="navbar-end">
<router-link to="/mobiles" class="navbar-item"><strong> Mobiles </strong></router-link>
<router-link to="/laptops" class="navbar-item"><strong> Laptops </strong></router-link> 

<div class="navbar-item">
<div class="buttons">
<router-link to="/login" class="button is-light"><strong> Login </strong></router-link> 
<router-link to="/signup" class="button is-light"><strong> Signup </strong></router-link> 
<router-link to="/signup" class="button is-success">
<span class="icon"> <i class="fas fa-shopping-cart"> </i>  {{cartTotalLength}} </span> <strong> </strong></router-link> 

</div>
</div>

</div>
</div>
</nav>
<section class="section">
  <router-view/>
</section>
<footer class="footer">
<p class="has-text-centered"> 
Developed by Shivam Rohilla 
</p>
</footer>
</div>
</template>
<script>
export default{
  data(){
    return{
     showMobileMenu: false,
     cart: {
       items: []
     }
    }
  },
  beforeCreate() {
    this.$store.commit('initializeStore')
  },
  mounted() {
    this.cart = this.$store.state.cart
  },
  computed: {
    cartTotalLength() {
      let totalLength = 0

      for(let i = 0; i < this.cart.items.length; i++) {totalLength += this.cart.items[i].quantity}
      return totalLength
    }
  }

  }
</script>
<style lang="scss">
@import '../node_modules/bulma';
</style>
