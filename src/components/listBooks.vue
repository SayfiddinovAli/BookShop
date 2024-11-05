<template >
    <div v-if="data?.length > 0">
     
        <input type="text" placeholder="Kitobni izlash" v-model="search">
        <table border="1" width="100%">
        <thead>
            <th>N</th>
            <th>Kitob nomi</th>
            <th>Kitob soni</th>
            <th>Kitob narxi</th>
            <th>Amallar</th>
        </thead>
        <tbody>
            <tr v-for="(book, index) of  filteredData">
                <td>{{ index +1 }}</td>
                <td>{{ book.name }}</td>
                <td>{{ book.price }}</td>
                <td>{{ book.count }}</td>
                <td><button @click="removeBook(book.id)">X</button></td>
            </tr>
        </tbody>

         <tfoot>
          <tr>
            <td colspan="5" align="right">Jami:
                {{ 
           filteredData?.reduce((total, item) => 
              total + (item.count || 0) * (item.price || 0), 0)
                }}



                </td>
          </tr>
         </tfoot>
        </table>
    </div>
</template>
<script>
export default {
    props:["data"],
     data() {
        return {
            search:''
        }
     },
    methods:{
        removeBook(id){
           if (confirm('Qaroringiz qatiymi?')) {
         this.$emit('removeBook',id)
           }
        }
    },
    computed:{
         filteredData(){
            return this.data.filter((item)=>
        item.name?.toLowerCase().includes(this.search?.toLowerCase()));
         }
    }
};
</script>
<style>
    
</style>