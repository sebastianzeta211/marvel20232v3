<template>
     <div >   

      <v-img :src="imagen" height="100px"
    width="150px">    </v-img>
    <h4 class="ml-4" v-if="Detailheroe.name != ''">Nombre->= {{ Detailheroe.name}}.</h4>
          <h4 class="ml-4" v-else>No se pudo obtener el nombre del heroe seleccionado.</h4>
<br>

<p class="ml-4" v-if="Detailheroe.description != ''">description->= {{ Detailheroe.description}}.</p>
          <p class="ml-4" v-else>No se pudo obtener description del heroe seleccionado.</p>
<br>


<h4 class="ml-4">-Comics= {{comics}}.</h4>
         
<br>



<h4 class="ml-4">-events= {{events}}.</h4>
         
<br>

<h4 class="ml-4">-stories= {{stories}}.</h4>
         
<br>

<h4 class="ml-4">-series= {{series}}.</h4>
         
<br>
<h3 class="ml-4">
            Nombre de las 3 primeras series:
            <br />
</h3>


<v-card-text v-for="item in primerasseries.slice(0, 3)" :key="item">
            *{{ item.name }}
          </v-card-text> 

          
          </div>




</template>
<script>

export default {
  name: 'DetailPage'
  ,

  data() {
    return {
      Detailheroe: [],imagen:"",comics:0,events:0,stories:0,series:0,primerasseries:[],id:1011334
    }
  }, mounted() {
    if (localStorage.getItem('cats')) {
      try {
        this.id=localStorage.getItem('cats');
         console.log('este es el id en local storage',localStorage.getItem('cats'));
      } catch(e) {
        localStorage.removeItem('cats');
      }
    }
  },

  created(){   
  // let i = this.obtener()
  console.log("que es esto",this.$route.params);

    const api ='https://gateway.marvel.com:443/v1/public/characters/'+this.id+'?ts=1&apikey=71fc19c18b1299bedd5c429e595365cc&hash=1a13f7c85ca4c7b330d3d16ba5ab87c5';
    fetch(api)
    .then(res=> {
      if(res.status==200){
       
        return res.json() 
    }else{
      //console.log(3)
    }
    } )
    .then((json)=>{
     // console.log(json)
    
      this.Detailheroe= json.data.results[0]
      this.imagen= this.Detailheroe.thumbnail.path + '.' + this.Detailheroe.thumbnail.extension
      if (this.Detailheroe.comics.available >0){
        this.comics = this.Detailheroe.comics.available
      }else{
        this.comics=0
      }
      ///////////////7      
      if (this.Detailheroe.events.available >0){
        this.events = this.Detailheroe.events.available
      }else{
        this.events=0
      }
       ///////////////7      
       if (this.Detailheroe.stories.available >0){
        this.stories = this.Detailheroe.stories.available
      }else{
        this.stories=0
      }
   ///////////////7      
   if (this.Detailheroe.series.available >0){
        this.series = this.Detailheroe.series.available
      }else{
        this.series=0
      }
///////////////////////////////
this.primerasseries= this.Detailheroe.series.items




      
    })


   
  }


}


</script>
