<template>
    <v-card title flat class="pa-md-10 pa-5 text-center" color="surface">
        <h2 class="text-md-6 font-weight-bold">FreeCommerce</h2>
        <div class="text-center">
            <v-btn v-for="(b,i) in sm" :key="i" color="surface" class="mr-2" fab depressed>
                <v-icon>{{ b.icon }}</v-icon>
            </v-btn>
    </div>
    </v-card>
   
</template>

<script>
    export default {
        data(){
            return{
                sm: [
        { icon: "mdi-facebook", link: "#" },
        { icon: "mdi-twitter", link: "#" },
        { icon: "mdi-instagram", link: "#" },
        { icon: "mdi-youtube", link: "#" },
      ],
            }
        }
    }
</script>

<style  scoped>

</style>