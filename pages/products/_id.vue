<template>
    <div>
        <Nav/>
        <v-container v-if="product" >
            <v-row justify="center">
                <v-col cols="11" md="7">
                    <h2 class="text-center text-md-h4 font-weight-bold">
                        {{ product.name }}
                    </h2>
                    <v-rating readonly half-increments class="mb-2 text-center"  color="yellow darken-2" background-color="grey lighten-1 " :value="product.ratings" dense-size="20">

                    </v-rating>
                   
                    <div class="tags">
                        <v-chip small label  outlined class="mr-1 text-center"  v-for="(t,i) in product.tags" :key="i">
                    {{ t }}
                 </v-chip>
                    </div>
                 <br/>
                 <v-img width="100%" class="el rounded-lg" height="50vh" :src="product.image"></v-img>
                 <p class="mt-5 mb-7">
                    {{ product.description }}
                 </p>
                 <v-btn @click="$store.commit('cart/AddToCart', product)" min-heights="45" min-width="170" class="text-capitalize" color="primary">Add to Cart</v-btn>
                </v-col> 
            </v-row>
        </v-container>
    </div>
</template>

<script>
    export default {
        async created(){ 
      const p = await this.$content('products').where({id: parseInt(this.$route.params.id)}).limit(1).fetch()
      this.product = p[0]
    },
    data(){
        return{
            product: null,
        }
    }
    }
</script>

<style scoped>
.tags{
    margin: auto;
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>