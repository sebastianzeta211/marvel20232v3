<template>
                                              

<div>
  <v-row>
    <v-col v-for="heroe in heroes" :key="heroe.id" class="text-center" >
      <a :href="'personaje/'+heroe.id" v-on:click="Redireccionar(heroe.id)">

      <v-img :src="heroe.thumbnail.path + '.' + heroe.thumbnail.extension" height="100px"
    width="150px"
          >
         
          </v-img>
      <blockquote class="blockquote">
        <p v-if="heroe.name !=='' ">{{ heroe.name }}</p>
            <p  v-else>sin nombre.</p>

        <footer>
          <small>
            <em v-if="heroe.description !=='' ">{{   heroe.description }}</em>
            <em  v-else>no description.</em>
          </small>
          <!-- Using value -->
  
        </footer>
      
      </blockquote>
    </a> 
    </v-col>
  </v-row>
  
  
</div>




  
</template>

<script>

export default {
  name: 'InspirePage'
  ,

  data() {
    return {
      heroes: [],
    }
  },
  created(){
    const api ='https://gateway.marvel.com:443/v1/public/characters?ts=1&apikey=71fc19c18b1299bedd5c429e595365cc&hash=1a13f7c85ca4c7b330d3d16ba5ab87c5';
    fetch(api)
    .then(res=> res.json())
    .then((json)=>{
     // console.log(json)
      this.heroes= json.data.results
      
    })

   
  },
  methods: {
    Redireccionar: function (id) {
    
      localStorage.setItem("cars", id);
 //console.log(id);
  }
}


}




</script>
