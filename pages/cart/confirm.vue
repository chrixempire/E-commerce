<template>
    <div>
        <Nav /> 
        <div v-if="$store.state.cart.cart.length == 0" class="text-center">
            <p>No items just yet. Keep Shopping</p>
        </div>
        <v-container>
            <div class="mb-3" v-if="$store.state.cart.cart.length > 0" > 
                <v-btn nuxt to="/cart"
                    min-width="150"
                    min-height="45"
                    depressed
                    
                >
                    Back
                </v-btn>
                <v-btn @click="process" min-width="150" min-height="45" color="primary">Complete</v-btn>

            </div>
            <v-form lazy-validation ref="form" class="mt-10">
        <p class="font-weight-bold">Personal & Delivery</p>
        <v-row>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="email"
              :rules="[rules.required, rules.email]"
              outlined
              label="Email"
              type="email"
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="name"
              :rules="[rules.required]"
              outlined
              label="Full Name"
              type="text"
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="phone"
              outlined
              label="Phone"
              type="tel"
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="address"
              :rules="[rules.required]"
              outlined
              label="Address"
              type="text"
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="city"
              :rules="[rules.required]"
              outlined
              label="City"
              type="text"
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="country"
              :rules="[rules.required]"
              outlined
              label="Country"
              type="text"
            ></v-text-field>
          </v-col>
        </v-row>
        <p class="font-weight-bold">Credit card</p>
        <v-row>
          <v-col cols="12" md="12">
            <v-text-field
              v-model="cc"
              :rules="[rules.required]"
              outlined
              label="Credit Card Number"
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="expdate"
              :rules="[rules.required]"
              outlined
              label="Exp date"
            ></v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="cvv"
              :rules="[rules.required]"
              outlined
              label="Security code/CVV"
            ></v-text-field>
          </v-col>
        </v-row>
      </v-form>
            
        </v-container>
    </div>
</template>

<script>
    export default {
        methods:{
            async process(){
                if(!this.$refs.form.validate())
                return;
                await this.$swal({
                    title:"processing your order",
                    icon: "info",
                    allowEscapekey: false,
                    allowOutsideClick: false,
                    timer:3000,
                    timeProgressBar:true,
                    text:"please wait",
                    sowConfirmButton: false,
                })
                await this.$swal({
                title:" Order Complete",
                    icon: "success",
                    allowEscapekey: false,
                    allowOutsideClick: false,
                    timer:4000,
                    timeProgressBar:true,
                    text:"Thank you for your patronage",
                    sowConfirmButton: false,
            });
            this.$store.commit("cart/clearCart");
            this.$router.push("/")
            }
       
        },
        data(){
            return{
                email:null,
                name:null,
                phone: null,
                address: null,
                city:null,
                country:null,
                cc: "424242424242",
                expdate: "06/15",
                cvv:"123",
                rules:{
                    required:(v)=> !!v || "Required",
                    email:(v)=>{
                            const pattern =  /^\w+@[a-zA-Z_]+?\.[a-zA-Z]{2,3}$/
                            return pattern.test(v) || "Invalid e-mail"
                    }
                }
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>