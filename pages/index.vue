<template>
  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">
            Id:
          </th>
          <th class="text-left">
            Nome:
          </th>
          <th class="text-left">
            Email:
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in request" @click.stop="loadUser(item.id)">
          <td>{{ item.id }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.email }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>

<script>


export default { 
  data(){
    return{
      request: null,
      url:"http://localhost:3000/users"
    }
  },

  methods:{
    async getUser(){
      const vm = this;
      try{
        const req = await this.$axios.get(vm.url)
        vm.request = req.data;
      }catch(err){
        alert('erro');
      }
    },
    loadUser(id){
      this.$router.push('/'+ id);
    }
  },
  mounted(){
    this.getUser();
  } 
}
</script>
