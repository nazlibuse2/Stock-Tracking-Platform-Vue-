<template>
  <div v-if="productList.length>0">
    <h3 class="text-center">Added Products</h3>
    <hr>
    <div class="row product-container">
        <app-product v-for="product in productList">
        <img class="card-img-top" :src="product.selectedImage" :alt="product.title">
        <div class="card-body">
          <h5 class="card-title">{{product.title}}</h5>
          <small><strong>Number : </strong> {{product.count}}</small>
          <br>
          <small><strong>Price : </strong> {{product.price}}</small>
          <br>
          <small><strong>Total : </strong> {{product.totalPrice}}</small>
        </div>
        </app-product>
    </div>
  </div>
</template>

<script>

import Product from './Product'
import {eventBus} from "../main";

export default {
    components:{
        appProduct:Product
    },
    data(){
      return{
        productList: [],
      }
    },
    created(){
      eventBus.$on("productAdded", (Product) => {
        if(this.productList.length<10){
          this.productList.push(Product);
          eventBus.$emit("progressBarUpdated",this.productList.length);
        }else{
          alert("You cannot add more products!");
        }
      });
    }
}
</script>
