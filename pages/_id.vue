<template>
  <div>
    <div class="escopo">   
        <div class="image">    
            <v-img 
                lazy-src="https://lh3.googleusercontent.com/proxy/1_Rjut8Pxr30tOhbTeZC7axjKYe2tfntU8jX3wOssEoysSMmIQLVymK-60iSTwZO2l0mGxV_lH864v_OkDWwxn_W6cIlIHVQ4gBRu_UI7jRYi7b5LrgibRYRZg"
                max-height="150"
                max-width="150"
                src="https://lh3.googleusercontent.com/proxy/1_Rjut8Pxr30tOhbTeZC7axjKYe2tfntU8jX3wOssEoysSMmIQLVymK-60iSTwZO2l0mGxV_lH864v_OkDWwxn_W6cIlIHVQ4gBRu_UI7jRYi7b5LrgibRYRZg"
            ></v-img>
        </div>    
        <h2 class="name">{{nome}}</h2>
        
    </div>
    <div class="d-flex flex-column mb-6">
      <v-card
        class="pa-2"
        outlined
        tile
      >
        <h3>Areas:</h3>
        </br>
        <p v-for="item in areas">{{item.name}}</p>

      </v-card>
    </div>
    <div class="d-flex flex-column mb-6">
      <v-card
        class="pa-2"
        outlined
        tile
      >
        <h3>Technologies:</h3></br>
         <p v-for="item in technologies">{{item.name}} - {{item.level}}</p>
      </v-card>
    </div>
    <div class="d-flex flex-column mb-6">
      <v-card
        class="pa-2"
        outlined
        tile
      >
        <h3>Experiences:</h3></br>
        <div v-for="item in experiences">
            <p>Empresa: {{item.companyName}}</p>
            <p>Inicio: {{item.startDate}}</p>
            <p>Fim: {{item.endDate}}</p>
            <p>Remuneração: {{item.remuneration}}</p>
            <hr>
            </br>
        </div>
      </v-card>
    </div>
  </div>
</template>

<script>
    export default { 
        data(){
            //layout
            return{
                id:null,
                url:"http://localhost:3000/users/",
                request: null,
                nome:'',
                areas:[],
                technologies:[],
                experiences:[]
          

            }
        },
        methods:{
            async getUser(){
                const vm = this;
                try{
                    const req = await this.$axios.get(vm.url + vm.id);
                    vm.request = req.data;
                    vm.nome = vm.request.name;
                    vm.areas = vm.request.aresa
                    vm.technologies = vm.request.technologies;
                    vm.experiences = vm.request.experiences;


                }catch(err){
                    alert('Erro');
                }
            }
        },
        mounted(){
            this.id = this.$route.params.id;
            this.getUser();
        }
    }   
</script>

<style>
    .escopo{
        display:inline-block;
        height:300px;
        width:100%;
        margin-bottom:2%;
        background-image: url("https://thumbs.dreamstime.com/b/ultra-papel-de-parede-do-mapa-mundo-da-tecnologia-sum%C3%A1rio-hd-112324892.jpg");
        background-size:100%;
        
    }
    .image{
        display:inline-block;
        position:relative;
        margin-top: 12%;
        margin-left:2%;
    }

    .name{
        display:inline-block;
        margin-left:2%;
    }

</style>