<template>
    <div>
        <Nav/>
        <br/>
        <div v-if="$store.state.cart.cart.length == 0" class="text-center">
            <p>No items just yet. Keep Shopping</p>
        </div>
        <v-container>
            <div class="mb-3" v-if="$store.state.cart.cart.length > 0" >
                <v-btn nuxt to="cart/confirm" min-width="150"
                min-height="45"
                color="primary"
                >Checkout</v-btn>
            </div>
            <v-row> 
                <template v-for="(c, i) in $store.state.cart.cart">
                    <v-col :key="i">
                        <v-card color="surface" flat>
                            <v-btn @click="$store.commit('cart/RemoveCartItem', i)"
                            absolute
                            top 
                            right
                            icon
                            > <v-icon size="18">
                                mdi-delete
                                </v-icon>
                                </v-btn>
                                <v-row dense>
                                    <v-col md="3">
                                        <v-img class="rounded-lg"
                                        height="220"
                                        :src="c.product.image"></v-img>
                                    </v-col>
                                    <v-col class="pl-5 pt-2" md="9">
                                        <h2 class="text-md-h6 font-weight-bold">{{ c.product.name}} X {{ c.quantity }}</h2>
                                        <p class="primary--text mt-2">
                                            {{ $formatMoney(c.product.price * c.quantity) }}
                                        </p>
                                        <v-btn @click="$store.commit('cart/IncreaseItemCount',i)" icon>
                                            <v-icon>mdi-plus-circle</v-icon>
                                        </v-btn>
                                        <span class="mx-2">{{ c.quantity }}</span>
                                        <v-btn @click="$store.commit('cart/DecreaseItemCount', i)" icon>
                                        <v-icon size="20">mdi-minus-circle</v-icon>
                                        </v-btn>
                                    </v-col>
                                </v-row>
                        </v-card>
                    </v-col>
                </template>
            </v-row>
        </v-container>
        <br/><br/>
        <Footer/>
        <ScrollTop/>
    </div>
</template>

<script>
    export default {
        
    }
</script>

<style lang="scss" scoped>

</style>