<template>
  <div v-for="(item, index) in pokemon.results" :key="index">
      <router-link :to="`/pokedex/${item.name}`">{{item.name}}</router-link>
  </div>
  <button @click="obtenerApi(obtenerPaginaAnterior)">Previous</button>
  <button @click="obtenerApi(obtenerPaginaProxima)">Next</button>
</template>

<script>
export default {
    data() {
        return {
            url:'https://pokeapi.co/api/v2/pokemon/',
            pokemon: {}
        }
    },
    methods: {
       async obtenerApi(url) {
           try {
               const data = await fetch(url)
                const res = await data.json()
                this.pokemon = res
                console.log(res)
           } catch (error) {
                console.log(error) 
           }
            
        },
        urlPoke(url){
            this.obtenerApi(url)
        }
       
    },
    created(){
        this.obtenerApi(this.url)
    },
    computed: {
        obtenerPaginaProxima() {
            return this.pokemon.next
        },
        obtenerPaginaAnterior() {
            return this.pokemon.previous
        }
    },
}
</script>

<style>

</style>
