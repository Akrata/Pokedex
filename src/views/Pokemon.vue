<template>
    <h1>{{poke.name}}</h1>
    <img :src="img" alt="">
    
    
</template>

<script>
export default {
    
    data() {
        return {
            poke: {},
            img:""
        }
    },
    
    methods: {
       async obtenerPoke() {
           try {
                const data = await fetch(`https://pokeapi.co/api/v2/pokemon/${this.$route.params.nombre}`)
                const res = await data.json()
                this.poke = res
                console.log(res)
                this.img = res.sprites.other.dream_world.front_default
                console.log(this.img)
           } catch (error) {
                console.log(error) 
           }
            
        },
    },
    created(){
        this.obtenerPoke()
    },
    computed: {
        imagen() {
            return this.poke.sprites.other.dream_world.front_default
        }
    },

}
</script>

<style>

</style>